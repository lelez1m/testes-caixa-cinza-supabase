# Testes de Caixa Cinza — Autenticação Supabase

**Aluno:** Alexandre de Jesus RA:251956  
**Curso:** Análise e Desenvolvimento de Sistemas — FACENS  
**Ferramentas:** Supabase, Postman Desktop e GitHub  
**Data dos testes:** 07/11/2026

## Introdução

Esta atividade apresenta a realização de testes de caixa cinza em uma API de autenticação. Foram utilizadas as ferramentas Supabase para gerenciamento dos usuários e autenticação, Postman Desktop para execução das requisições HTTP e GitHub para documentação dos resultados.

Os testes de caixa cinza permitem verificar o funcionamento de um sistema conhecendo parcialmente sua estrutura, como endpoints, headers, métodos HTTP e respostas JSON.

## Objetivo da Atividade

O objetivo foi configurar um ambiente de autenticação por e-mail e senha, executar testes funcionais na API e verificar se o sistema aceita credenciais válidas e rejeita tentativas de acesso inválidas.

Foram executados cinco cenários de teste, analisando os códigos HTTP, as respostas JSON, as mensagens de erro e a geração do token de autenticação.

## Configuração do Supabase

Foi criado um projeto na plataforma Supabase com o nome **Testes-Caixa-Cinza-ADS**, utilizando o plano gratuito.

A autenticação escolhida foi por e-mail e senha. A confirmação obrigatória de e-mail foi desativada para facilitar a execução dos testes no ambiente acadêmico.

Na seção Authentication, foi cadastrado um usuário de teste com e-mail e senha, utilizado posteriormente nas requisições do Postman.

Também foram identificadas a URL do projeto e a chave pública da API, necessárias para realizar as requisições de autenticação.

O objetivo dessa configuração foi disponibilizar um serviço de autenticação funcional para verificar o comportamento da API.

## Configuração do Postman

Foi utilizado o Postman Desktop para executar os testes.

Foi criado o Workspace **Testes Caixa Cinza Supabase** e um Environment chamado **Ambiente Supabase ADS**.

As seguintes variáveis foram configuradas:

| Variável | Finalidade |
|---|---|
| base_url | Endereço principal da API Supabase |
| api_key | Chave pública da API |
| email | E-mail do usuário cadastrado |
| password | Senha do usuário de teste |

O uso de variáveis facilitou a organização dos testes, evitando a necessidade de repetir as credenciais em cada requisição.

Foi criada a Collection **Testes API Autenticacao**, contendo cinco requisições para validação do login.

## Configuração das Requisições

As requisições utilizaram o método HTTP **POST**, responsável por enviar as credenciais do usuário ao servidor.

**Endpoint utilizado:**

`{{base_url}}/auth/v1/token?grant_type=password`

**Headers configurados:**

| Header | Valor |
|---|---|
| apikey | {{api_key}} |
| Content-Type | application/json |

A autenticação da requisição inicial foi configurada como No Auth, utilizando a chave publicável do Supabase no header apikey. O endpoint retorna um access_token quando o login é realizado com sucesso, permitindo o uso posterior de Authorization no formato Bearer Token.

**Exemplo do Body JSON:**

```json
{
  "email": "{{email}}",
  "password": "{{password}}"
}
```

A finalidade dessa requisição foi verificar se a API permite autenticação com credenciais corretas e bloqueia tentativas com informações incorretas.

## Execução dos Testes

Foram realizados cinco cenários de testes de autenticação utilizando o Postman Desktop.

| Cenário | Entrada utilizada | Resultado esperado | Resultado obtido | Status |
|---|---|---|---|---|
| CT01 — Login válido | E-mail e senha corretos | HTTP 200 e access_token | HTTP 200 e token retornado | Sucesso |
| CT02 — Senha incorreta | E-mail correto e senha errada | Erro de autenticação | HTTP 400 — invalid_credentials | Sucesso |
| CT03 — Usuário inexistente | E-mail não cadastrado | Acesso negado | HTTP 400 — invalid_credentials | Sucesso |
| CT04 — Campos vazios | E-mail e senha vazios | Erro de validação | HTTP 400 — validation_failed | Sucesso |
| CT05 — Credenciais inválidas | E-mail malformado e senha inválida | Mensagem de erro | HTTP 400 — invalid_credentials | Sucesso |

**CT01 — Login válido:** a API retornou HTTP 200 OK e gerou um access_token, confirmando o funcionamento da autenticação.

**CT02 — Senha incorreta:** a API retornou HTTP 400 Bad Request, com a mensagem "Invalid login credentials".

**CT03 — Usuário inexistente:** a API retornou HTTP 400 Bad Request, impedindo o acesso de um usuário não cadastrado.

**CT04 — Campos vazios:** a API retornou HTTP 400 Bad Request, com o código validation_failed e a mensagem "missing email or phone".

**CT05 — Credenciais inválidas:** a API retornou HTTP 400 Bad Request, com o código invalid_credentials e a mensagem "Invalid login credentials".

## Registro dos Testes

Os testes foram documentados em uma planilha Excel contendo identificação, cenário, entrada, resultado esperado, resultado obtido, status e observações.

A planilha permite comparar o comportamento esperado com o resultado apresentado pela API.

Os registros foram organizados utilizando as respostas reais obtidas durante a execução das requisições no Postman.

Os cinco cenários apresentaram os comportamentos esperados, sem falhas funcionais identificadas nos cenários executados.

A planilha está disponível na pasta **planilha/** do repositório, enquanto as capturas de tela dos testes estão organizadas na pasta **prints/**.

## Resultados Obtidos

Foram executados cinco cenários de autenticação, sendo um positivo e quatro negativos.

**Total de testes:** 5  
**Testes com resultado esperado:** 5  
**Falhas funcionais identificadas:** 0  
**Taxa de sucesso dos cenários:** 100%

O login válido retornou HTTP 200 e um token de acesso.

As quatro tentativas inválidas retornaram HTTP 400, acompanhadas de mensagens de erro, demonstrando que a API rejeitou as entradas incorretas utilizadas.

Os resultados indicam que a autenticação apresentou o comportamento esperado nos cenários avaliados.

## Conclusão

A atividade permitiu compreender o funcionamento de testes de caixa cinza aplicados a APIs de autenticação.

A configuração do Supabase foi concluída e o Postman permitiu executar os cinco cenários de teste.

Durante a execução, foram observadas respostas HTTP 200 para o login válido e HTTP 400 para as tentativas inválidas.

Uma das dificuldades encontradas foi a configuração inicial do Postman, especialmente na definição das variáveis do Environment e na organização das requisições.

Não foram identificadas falhas funcionais nos cenários executados. Como possibilidades de melhoria, poderiam ser implementados testes automatizados, validação de tokens expirados, testes de segurança e novos cenários de autenticação.

Os testes de caixa cinza são importantes porque permitem analisar o comportamento de uma API utilizando conhecimento parcial de sua estrutura, facilitando a identificação de erros e contribuindo para a qualidade e confiabilidade do software.
