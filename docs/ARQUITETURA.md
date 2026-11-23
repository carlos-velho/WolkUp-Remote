# Arquitetura inicial — WolkUp Remote

Status: planejamento técnico, sem binários compilados.

## Objetivo
Aplicação Windows x64 de assistência remota com interface Cliente e Gerenciador, baseada no RustDesk de código aberto.

## Fases
1. Validar licença, versão upstream e processo de compilação.
2. Construir um protótipo funcional sem mudanças no motor de conexão.
3. Separar a experiência Cliente/Gerenciador, mantendo controles de autenticação.
4. Adicionar identidade visual oficial somente após receber os arquivos originais.
5. Testar acesso assistido, instalação, serviço, acesso não assistido, transferência de arquivos e desinstalação.

## Restrições
- Não modificar a VPS Hostinger nem NetBird nesta fase.
- Não publicar um cliente como produto final sem testes reais.
- Não prometer exclusividade de conexão apenas por ocultar botões na interface.
- O acesso não assistido exige consentimento e credenciais fortes.
- Não registrar senhas, tokens ou chaves no repositório.
- Respeitar a licença do RustDesk e preservar avisos de copyright e obrigações de disponibilização do código-fonte.
- Não renomear binários de terceiros para sugerir que já são uma compilação própria.

## Referência
- Código upstream: https://github.com/rustdesk/rustdesk
- Fluxos de build upstream: https://github.com/rustdesk/rustdesk/tree/master/.github/workflows
