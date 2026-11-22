# Somativa de Backend, DevOps e Computação em Nuvem

Dois projetos Java 21 com Spring Boot desenvolvidos para a somativa da Aula 11. Cada API tem seu próprio código, testes, Dockerfile e relatório.

| Exercício | Porta local | Documentação |
| --- | --- | --- |
| Monitoramento de máquinas | 8080 | [Endpoints e execução](exercicio1-monitoramento-maquinas/README.md) · [Relatório](exercicio1-monitoramento-maquinas/RELATORIO.md) |
| Biblioteca | 8081 | [Endpoints e execução](exercicio2-biblioteca/README.md) · [Relatório](exercicio2-biblioteca/RELATORIO.md) |

## Compilar e testar

Com JDK 21 e Maven 3.9, rode na raiz do repositório:

```powershell
mvn -B verify
```

O Maven roda os testes JUnit 5 e MockMvc dos dois projetos e gera um JAR em cada pasta `target`.

## Executar as APIs

Abra dois terminais na raiz do repositório e rode um comando em cada um:

```powershell
mvn -f exercicio1-monitoramento-maquinas/pom.xml spring-boot:run
mvn -f exercicio2-biblioteca/pom.xml spring-boot:run
```

O monitoramento responde em `http://localhost:8080/status`. A documentação da biblioteca responde em `http://localhost:8081/documentacao`. Os roteiros manuais estão nos arquivos `tests/requisicoes.http` de cada exercício.

## GitHub Actions e Railway

O [workflow da somativa](.github/workflows/pipeline.yml) compila e testa os dois projetos em Java 21 e disponibiliza os JARs e os relatórios de teste. Veja as [execuções do GitHub Actions](https://github.com/recheraphael-Re/Somativa-Backend-Devops-Nuvem/actions).

Para publicar no Railway, use dois serviços vinculados a este repositório. Defina o **Root Directory** de cada serviço como `/exercicio1-monitoramento-maquinas` ou `/exercicio2-biblioteca`. Ambos aceitam a variável `PORT`. Os relatórios registram quais capturas e links ainda precisam ser anexados.

## Projetos de origem

As correções antes da consolidação estão documentadas nos [pull requests de máquinas](https://github.com/recheraphael-Re/aula11desbEX1_nota/pull/1) e [de biblioteca](https://github.com/recheraphael-Re/aula11desbEX2_nota/pull/1).
