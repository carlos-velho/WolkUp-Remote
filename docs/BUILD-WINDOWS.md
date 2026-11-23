# Compilação Windows — plano de execução verificável

## Base selecionada
- Upstream: https://github.com/rustdesk/rustdesk
- Versão: 1.5.3
- Commit: `95cca3f661f635b3cc85c04935fe8d96d8f432ef`
- Licença upstream: AGPL-3.0, arquivo `LICENCE`
- Fluxo upstream: `.github/workflows/flutter-build.yml`

## Situação
O repositório WolkUp-Remote contém documentação e validação de fonte, mas **não contém o código-fonte do cliente RustDesk nem workflow de compilação Windows**. O fluxo de validação aprovado não produz EXE.

## Caminho recomendado
1. Criar fork de `rustdesk/rustdesk` em `carlos-velho`, com histórico e submódulos preservados, ou importar o código completo para uma branch de desenvolvimento.
2. Fixar versão e conferir submódulos/dependências; copiar e adaptar os workflows oficiais para compilar Windows x64.
3. Executar CI e registrar logs, checksums e artefatos; não distribuir binários sem validar a procedência.
4. Fazer alterações de marca e separar Cliente/Gerenciador, preservando controles de autorização e licenciamento.
5. Testar com dois PCs Windows, incluindo UAC, serviço, bandeja, NAT, transferências, revogação e desinstalação.
6. Distribuir somente após revisão de licença, segurança e testes.

## Restrições
- Não apresentar um executável RustDesk original renomeado como WolkUp Remote.
- Não anunciar segurança, exclusividade ou ausência de defeitos sem testes.
- Não modificar VPS, NetBird ou serviços existentes para executar esta etapa.
