# Relatório de entrega — Biblioteca

- **Nome:** preencher
- **RA:** preencher
- [Repositório](https://github.com/recheraphael-Re/Somativa-Backend-Devops-Nuvem) · [Commits](https://github.com/recheraphael-Re/Somativa-Backend-Devops-Nuvem/commits/main/) · [Pull requests](https://github.com/recheraphael-Re/Somativa-Backend-Devops-Nuvem/pulls?q=is%3Apr) · [GitHub Actions](https://github.com/recheraphael-Re/Somativa-Backend-Devops-Nuvem/actions)

## 1. API e validação local

A API gerencia o acervo de livros, valida os status `Disponível` e `Emprestado` e grava o catálogo em JSON. Os dados são recuperados na inicialização. O endpoint `/documentacao` lista as rotas e o [README](README.md#2-endpoints) descreve métodos, campos e códigos esperados.

| Requisição exercitada localmente | Resultado |
| --- | --- |
| `GET /` | 200, boas-vindas |
| `GET /livros` | 200, listagem do acervo |
| `POST /livros/cadastrar` | 201, cadastro com ID |
| `GET /livros/{id}` | 200, livro encontrado |
| `PUT /livros/alterar/{id}` | 200, dados atualizados |
| `GET /livros/999999` | 404, ID inexistente |
| `GET /documentacao` | 200, lista dos endpoints |

O Maven `verify` com Java 21 gerou `biblioteca-1.0.0.jar`. Os **9 testes JUnit 5 com MockMvc** passaram. A validação com o JAR em execução confirmou que o ano e o status alterados foram restaurados do JSON após reiniciar a aplicação.

O [código dos testes](src/test/java/br/com/cloudtech/ApplicationTest.java) cobre os sete cenários pedidos, mais validação dos campos e recuperação de dados do arquivo. Para reproduzir, execute `mvn -B verify` e consulte `target/surefire-reports/`.

## 2. Integração contínua e deploy

O [workflow](../.github/workflows/pipeline.yml) usa Java 21, baixa as dependências, compila, executa os testes e disponibiliza o JAR e os relatórios do Surefire. A publicação no Railway usa o repositório GitHub conectado à branch `main`, com o diretório `/exercicio2-biblioteca` como raiz do serviço. A API lê a porta de `PORT` e, com **Wait for CI** ativado no Railway, o deploy aguarda a aprovação do GitHub Actions. [Configuração de deploy automático](https://docs.railway.com/deployments/github-autodeploys)

## 3. Evidências para anexar

- [ ] Captura da execução aprovada dos testes automatizados e do GitHub Actions.
- [ ] Capturas dos sete cenários no Thunder Client, incluindo HTTP 404, com método, URL, status e resposta. Use o [roteiro das requisições](tests/requisicoes.http).
- [ ] URL pública do Railway e capturas do Thunder Client repetindo os testes na API publicada.
