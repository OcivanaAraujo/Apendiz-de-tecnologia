# Git e GitHub — Guia Prático de Aprendizado

> Registro dos fundamentos de Git e GitHub praticados no repositório **Aprendiz-de-Tecnologia**.

---

## 1. O que é Git e GitHub?

### Git

O **Git** é um sistema de controle de versão distribuído. Ele permite registrar alterações nos arquivos de um projeto, consultar o histórico, criar ramificações e recuperar versões anteriores.

### GitHub

O **GitHub** é uma plataforma que hospeda repositórios Git remotamente. Ele permite armazenar projetos, colaborar, revisar alterações por Pull Requests e manter uma cópia remota do projeto.

### Relação básica

```text
💻 Computador
     │
     │ Git
     ↓
🌐 GitHub
```

O Git trabalha localmente no computador. O GitHub funciona como um repositório remoto.

---

# 2. Configuração inicial do Git

Depois da instalação do Git, é necessário configurar a identidade que será utilizada nos commits.

## 2.1 Verificar a instalação

```bash
git --version
```

Exemplo:

```text
git version 2.55.0.windows.3
```

---

## 2.2 Configurar o nome global

```bash
git config --global user.name "Seu Nome"
```

Exemplo:

```bash
git config --global user.name "Ocivana Araujo"
```

O parâmetro `--global` faz com que essa configuração seja utilizada como padrão nos repositórios do computador.

---

## 2.3 Configurar o e-mail global

Utilizar o e-mail associado à conta do GitHub:

```bash
git config --global user.email "seu-email@example.com"
```

---

## 2.4 Conferir a configuração

```bash
git config --global --list
```

Deve aparecer algo semelhante a:

```text
user.name=Seu Nome
user.email=seu-email@example.com
```

### Resumo da configuração global

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@example.com"
git config --global --list
```

---

# 3. Clonar um repositório do GitHub

Para trabalhar localmente com um repositório que já existe no GitHub:

```bash
git clone URL_DO_REPOSITORIO
```

Exemplo:

```bash
git clone https://github.com/USUARIO/REPOSITORIO.git
```

O `clone` baixa o repositório para o computador e configura automaticamente o repositório remoto, normalmente chamado de `origin`.

---

# 4. Entrar na pasta do projeto

Depois do clone:

```bash
cd NOME-DA-PASTA
```

Exemplo:

```bash
cd Apendiz-de-tecnologia
```

> O nome da pasta local pode ser diferente do nome atual do repositório no GitHub.

---

# 5. Verificar o estado do projeto

O comando mais importante para começar qualquer operação é:

```bash
git status
```

Ele informa:

* branch atual;
* se o projeto está sincronizado;
* arquivos modificados;
* arquivos preparados para commit;
* alterações ainda não registradas.

Exemplo de projeto limpo:

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

---

# 6. Verificar o repositório remoto

```bash
git remote -v
```

Exemplo:

```text
origin  https://github.com/USUARIO/REPOSITORIO.git (fetch)
origin  https://github.com/USUARIO/REPOSITORIO.git (push)
```

### `origin`

É o nome padrão utilizado pelo Git para identificar o repositório remoto principal.

### `fetch`

Endereço utilizado para buscar informações do repositório remoto.

### `push`

Endereço utilizado para enviar alterações ao repositório remoto.

---

# 7. Alteração do endereço remoto

Se o repositório for renomeado no GitHub, não é necessário clonar novamente.

Pode-se atualizar o endereço:

```bash
git remote set-url origin NOVA_URL
```

Exemplo:

```bash
git remote set-url origin https://github.com/USUARIO/Aprendiz-de-Tecnologia.git
```

Depois, conferir:

```bash
git remote -v
```

---

# 8. O ciclo básico do Git

O fluxo fundamental aprendido foi:

```text
EDITAR
   ↓
git status
   ↓
git add
   ↓
git commit
   ↓
git push
   ↓
GITHUB
```

Cada etapa possui uma finalidade diferente.

---

# 9. `git diff`

O comando:

```bash
git diff
```

mostra as alterações realizadas no arquivo que ainda não foram adicionadas à staging area.

Exemplo:

```text
- linha removida
+ linha adicionada
```

### Significados

```text
- = linha removida
+ = linha adicionada
```

É uma ferramenta importante para revisar uma alteração antes do commit.

---

# 10. `git add`

Depois de revisar a alteração:

```bash
git add README.md
```

O comando coloca o arquivo na **staging area**.

Também é possível adicionar todas as alterações:

```bash
git add .
```

### Fluxo

```text
Arquivo modificado
       ↓
    git add
       ↓
Staging Area
```

A staging area representa as alterações que serão incluídas no próximo commit.

---

# 11. `git commit`

O commit registra uma alteração no histórico local do Git.

Exemplo:

```bash
git commit -m "docs: atualiza README"
```

A opção `-m` permite informar a mensagem do commit.

### Fluxo

```text
Staging Area
     ↓
git commit
     ↓
Histórico do Git
```

Uma boa mensagem de commit deve ser curta e indicar claramente o que foi alterado.

Exemplos:

```text
docs: atualiza README
docs: adiciona fundamentos de Git
docs: corrige documentação
feat: adiciona novo projeto
fix: corrige erro de documentação
```

---

# 12. `git push`

O `git push` envia os commits locais para o repositório remoto.

```bash
git push
```

Fluxo:

```text
💻 Computador
     │
     │ git push
     ↓
🌐 GitHub
```

Exemplo de resultado:

```text
main -> main
```

Isso indica que os commits foram enviados para a branch correspondente no GitHub.

---

# 13. `git pull`

O `git pull` busca alterações do repositório remoto e atualiza a cópia local.

```bash
git pull
```

Fluxo:

```text
🌐 GitHub
     │
     │ git pull
     ↓
💻 Computador
```

Quando não existem alterações novas:

```text
Already up to date.
```

Quando existem alterações novas, o Git atualiza o histórico e os arquivos locais.

---

# 14. Diferença entre `push` e `pull`

| Comando     | Direção             | Finalidade                                      |
| ----------- | ------------------- | ----------------------------------------------- |
| `git push`  | Computador → GitHub | Enviar commits                                  |
| `git pull`  | GitHub → Computador | Trazer alterações                               |
| `git fetch` | GitHub → Git        | Buscar informações sem integrar automaticamente |

---

# 15. Branches

Uma **branch** é uma linha independente de desenvolvimento.

A branch principal normalmente é:

```text
main
```

Podemos criar uma branch para desenvolver uma alteração:

```bash
git branch aprendizado-git
```

Esse comando cria a branch, mas não muda para ela.

---

# 16. Listar branches

```bash
git branch
```

Exemplo:

```text
  aprendizado-git
* main
```

O `*` indica a branch atual.

Para visualizar branches locais e remotas:

```bash
git branch -a
```

---

# 17. Trocar de branch

```bash
git switch aprendizado-git
```

Depois:

```bash
git branch
```

Resultado esperado:

```text
* aprendizado-git
  main
```

Agora os novos commits serão feitos na branch `aprendizado-git`.

---

# 18. Criar e mudar para uma branch em um único comando

Uma forma mais prática é:

```bash
git switch -c nome-da-branch
```

Exemplo:

```bash
git switch -c novo-projeto
```

Esse comando:

1. cria a branch;
2. muda imediatamente para ela.

---

# 19. Enviar uma nova branch para o GitHub

Quando uma branch local ainda não possui uma branch correspondente no GitHub:

```bash
git push -u origin aprendizado-git
```

O `-u` estabelece a relação de acompanhamento entre:

```text
aprendizado-git
       ↓
origin/aprendizado-git
```

Depois disso, futuros `git push` e `git pull` podem ser utilizados de forma mais simples.

---

# 20. Pull Request

O **Pull Request (PR)** é uma proposta para integrar alterações de uma branch em outra.

Exemplo:

```text
aprendizado-git
       ↓
Pull Request
       ↓
main
```

O PR permite:

* revisar alterações;
* visualizar arquivos modificados;
* discutir mudanças;
* verificar o código;
* aprovar;
* fazer o merge.

### Fluxo praticado

```text
main
 ↓
criar branch
 ↓
alterar arquivo
 ↓
git add
 ↓
git commit
 ↓
git push
 ↓
Pull Request
 ↓
revisão
 ↓
Merge
 ↓
main
```

---

# 21. Merge

O **merge** integra o histórico de uma branch em outra.

No exercício:

```text
aprendizado-git
       ↓
     merge
       ↓
      main
```

O Git criou o commit:

```text
27da139 Merge pull request #1 from OcivanaAraujo/aprendizado-git
```

---

# 22. Como visualizar o histórico

Um comando muito útil:

```bash
git log --oneline
```

Ele mostra os commits de forma resumida.

Para visualizar também a estrutura de branches:

```bash
git log --oneline --graph --decorate --all
```

Exemplo:

```text
*   27da139 Merge pull request #1
|\
| * 14f0f91 docs: testa branch de aprendizado
|/
* fd293d4 Add synchronization test note to README
```

### Elementos importantes

```text
27da139
```

→ identificador do commit.

```text
HEAD -> main
```

→ indica que o HEAD está apontando para a branch `main`.

```text
origin/main
```

→ referência da branch `main` no repositório remoto.

```text
|\ 
|/
```

→ representação gráfica de uma ramificação e posterior integração.

---

# 23. HEAD

`HEAD` representa a posição atual do Git no histórico.

Quando aparece:

```text
HEAD -> main
```

significa que o trabalho atual está na branch `main`.

---

# 24. Excluir uma branch local

Depois que uma branch foi integrada e não é mais necessária:

```bash
git branch -d aprendizado-git
```

A opção `-d` realiza uma exclusão segura.

O Git verifica se a branch pode ser removida.

---

# 25. Excluir uma branch remota

Para remover a branch do GitHub:

```bash
git push origin --delete aprendizado-git
```

Isso remove a branch do repositório remoto.

---

# 26. Atualizar referências remotas

Depois de excluir uma branch no GitHub:

```bash
git fetch --prune
```

O `--prune` remove referências locais para branches remotas que já não existem no servidor.

Depois podemos conferir:

```bash
git branch -a
```

---

# 27. O que é `git fetch`?

```bash
git fetch
```

Busca informações novas do repositório remoto, mas não integra automaticamente essas alterações à branch atual.

É útil para consultar o estado do remoto antes de decidir o que fazer.

---

# 28. `git status` como comando de segurança

Uma boa prática é utilizar:

```bash
git status
```

antes e depois de operações importantes.

Exemplo:

```text
git status
git add README.md
git status
git commit -m "docs: atualiza README"
git status
git push
git status
```

Isso ajuda a entender exatamente em que estado o projeto está.

---

# 29. Comandos fundamentais aprendidos

| Comando                                      | Significado                          |
| -------------------------------------------- | ------------------------------------ |
| `git --version`                              | Verifica a versão instalada          |
| `git config --global user.name`              | Configura nome global                |
| `git config --global user.email`             | Configura e-mail global              |
| `git config --global --list`                 | Lista configurações globais          |
| `git clone URL`                              | Clona um repositório                 |
| `cd pasta`                                   | Entra em uma pasta                   |
| `git status`                                 | Mostra o estado do projeto           |
| `git remote -v`                              | Mostra os repositórios remotos       |
| `git remote set-url origin URL`              | Altera o endereço remoto             |
| `git diff`                                   | Mostra alterações não preparadas     |
| `git add arquivo`                            | Adiciona arquivo à staging area      |
| `git add .`                                  | Adiciona alterações ao staging       |
| `git commit -m "mensagem"`                   | Registra alterações                  |
| `git push`                                   | Envia commits ao GitHub              |
| `git pull`                                   | Traz alterações do GitHub            |
| `git fetch`                                  | Busca informações do remoto          |
| `git fetch --prune`                          | Atualiza e limpa referências remotas |
| `git branch`                                 | Lista branches locais                |
| `git branch nome`                            | Cria uma branch                      |
| `git switch nome`                            | Muda de branch                       |
| `git switch -c nome`                         | Cria e muda para uma branch          |
| `git branch -a`                              | Lista branches locais e remotas      |
| `git log --oneline`                          | Mostra histórico resumido            |
| `git log --oneline --graph --decorate --all` | Mostra histórico gráfico             |
| `git branch -d nome`                         | Exclui branch local                  |
| `git push origin --delete nome`              | Exclui branch remota                 |

---

# 30. Fluxo recomendado para alterações simples

Quando estiver trabalhando diretamente na branch apropriada:

```bash
git status
```

Editar os arquivos.

Depois:

```bash
git diff
```

Revisar as alterações.

Em seguida:

```bash
git add .
```

Conferir:

```bash
git status
```

Criar o commit:

```bash
git commit -m "tipo: descreve a alteração"
```

Enviar:

```bash
git push
```

Por fim:

```bash
git status
```

O objetivo é terminar com:

```text
nothing to commit, working tree clean
```

---

# 31. Fluxo recomendado com branch

Para uma alteração que merece uma branch própria:

```bash
git switch main
git pull
git switch -c nome-da-branch
```

Trabalhar nos arquivos.

Depois:

```bash
git status
git diff
git add .
git commit -m "tipo: descreve a alteração"
git push -u origin nome-da-branch
```

No GitHub:

```text
Pull Request
    ↓
Revisão
    ↓
Merge
```

Depois de integrar:

```bash
git switch main
git pull
git branch -d nome-da-branch
git push origin --delete nome-da-branch
git fetch --prune
```

---

# 32. O que foi aprendido na prática

Durante este aprendizado foram praticados conceitos fundamentais:

* instalação e verificação do Git;
* configuração global do usuário;
* configuração do e-mail;
* clonagem de repositório;
* relação entre Git local e GitHub;
* repositório remoto (`origin`);
* alteração de URL remota;
* `git status`;
* `git diff`;
* staging area;
* commits;
* mensagens de commit;
* `git push`;
* `git pull`;
* sincronização local/remota;
* criação de branches;
* troca de branches;
* envio de branches ao GitHub;
* Pull Request;
* revisão de alterações;
* Merge;
* histórico de commits;
* `HEAD`;
* `origin/main`;
* exclusão de branches locais;
* exclusão de branches remotas;
* `git fetch --prune`;
* leitura do gráfico de histórico.

---

# 33. Modelo mental para memorizar

```text
                    GITHUB
                      🌐
                      │
                 git pull
                      ↓
                    💻
                 COMPUTADOR
                      │
                  editar
                      ↓
                 git status
                      ↓
                   git diff
                      ↓
                  git add
                      ↓
                 git commit
                      ↓
                  git push
                      │
                      ↓
                    🌐
                   GITHUB
```

Quando houver uma branch:

```text
                 main
                  │
                  └──────→ nova-branch
                              │
                           alterações
                              │
                            commit
                              │
                             push
                              ↓
                         Pull Request
                              │
                            revisão
                              │
                            Merge
                              ↓
                            main
```

---

# 34. Regra prática

Antes de qualquer alteração importante:

```bash
git status
git pull
```

Depois de trabalhar:

```bash
git status
git diff
git add .
git commit -m "mensagem"
git push
```

E, ao terminar:

```bash
git status
```

O objetivo é saber sempre:

> **Onde estou? O que mudou? O que será registrado? E para onde essa alteração será enviada?**

Esse entendimento é mais importante do que decorar comandos isolados.

---

## 35. Próximos assuntos recomendados

Depois destes fundamentos, a sequência natural de aprendizagem é:

1. `.gitignore`
2. Convenções de mensagens de commit
3. Markdown aplicado ao GitHub
4. Branches com maior profundidade
5. Merge e conflitos
6. Rebase — posteriormente
7. Tags e releases
8. GitHub Issues
9. GitHub Projects
10. GitHub Actions
11. SSH para GitHub
12. Organização profissional de repositórios
13. Documentação de projetos
14. Versionamento de projetos reais

---

## Conclusão

O objetivo deste estudo não é apenas memorizar comandos.

O principal aprendizado é compreender o **fluxo de versionamento**:

```text
Alterar
  ↓
Revisar
  ↓
Preparar
  ↓
Registrar
  ↓
Sincronizar
  ↓
Revisar/Integrar
```

Git permite controlar o histórico localmente, enquanto GitHub possibilita armazenar, compartilhar e colaborar sobre esse histórico remotamente.

O conhecimento adquirido neste exercício constitui a base para utilizar Git e GitHub em projetos de estudo, portfólio e desenvolvimento de software.
