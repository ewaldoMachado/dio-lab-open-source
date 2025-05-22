# Agente de respostas

Com **GitHub Actions**, você pode automatizar respostas para interações no seu repositório. Aqui está um passo a passo para criar um agente de respostas

# Criar um agente de respostas com GitHub Actions.

# 1 - Criar um arquivo de Workflow.

No seu repositório, vá até a pasta .github/, crie uma pasta workflows e nela crie um arquivo YAML, por exemplo, responder-issues.yml.

# 2 - Definir o gatilho do workflow.

O agente pode ser acionado quando uma *issue* for aberta. No arquivo YAML, adicione:

name: Responder Issues
on:
  issues:
    types: [opened]

jobs:
  responder:
    runs-on: ubuntu-latest
    steps:
      - name: Responder à Issue
        uses: actions/github-script@v6
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          script: |
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: "Olá! Obrigado por abrir esta issue. Nossa equipe analisará e responderá em breve. 🚀"
            });

# 3 - Configurar o repositório

Certifique-se de que a pasta .github/workflows/ existe no seu repositório.

O **GitHub Token** já está disponível por padrão para interações básicas.

# 4 - Testar e ativar

Faça o ***Commit*** e o ***push*** do arquivo YAML para o repositório.

Abra uma issue e veja o agente responder automaticamente!

Não esqueça de fechar a **issue**. 