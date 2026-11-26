# WolkUp Remote para Windows x64

WolkUp Balanças, Automação Comercial e Tecnologia

## Abrir ou instalar

Extraia os artefatos da execução de homologação e compare o SHA-256 antes de executar. Use `Get-FileHash .\WolkUpRemote-Cliente.exe -Algorithm SHA256` e compare com `SHA256SUMS.txt`. Os executáveis desta etapa são sem assinatura digital.

- Abra `WolkUpRemote-Cliente.exe` no computador atendido. Informe o ID ao técnico e confira a solicitação antes de aceitá-la. Encerre a sessão pela janela de atendimento.
- Abra `WolkUpRemote-Gerenciador.exe` em uma conta autorizada do Windows. Informe o ID do computador atendido e solicite a conexão.
- Use os arquivos com sufixo `-install.exe` para abrir o instalador integrado. No Cliente, confira o serviço e o ícone da bandeja após a instalação. Para remover, use **Aplicativos instalados** nas configurações do Windows.
- Para habilitar acesso não assistido, o responsável pelo Cliente deve configurar uma senha exclusiva e aleatória com pelo menos 16 caracteres e alterar o modo de aprovação. Para revogar, encerre a sessão, volte à aprovação por clique e remova a senha permanente.

## Autorizar o técnico neste PC

Abra o PowerShell x64 como administrador. Substitua `NOME-DA-CONTA` pela conta do técnico. A configuração vale para este PC. O Gerenciador consulta o grupo autorizado no registro do sistema antes de cada nova sessão.

```powershell
$group = Get-LocalGroup -Name 'WolkUpRemoteTecnicos' -ErrorAction SilentlyContinue
if (!$group) { $group = New-LocalGroup -Name 'WolkUpRemoteTecnicos' }
Add-LocalGroupMember -Group $group.Name -Member 'NOME-DA-CONTA'
$key = 'HKLM:\SOFTWARE\WolkUp\Remote'
New-Item -Path $key -Force | Out-Null
New-ItemProperty -Path $key -Name OperatorGroupSid -Value $group.SID.Value -PropertyType String -Force | Out-Null
```

O técnico deve sair da sessão do Windows e entrar novamente para atualizar o token. Para revogar um técnico, remova-o do grupo, encerre os atendimentos abertos e termine a sessão Windows dessa conta. A autorização local do operador e a aprovação do lado do Cliente são controles independentes.

## Internet

O servidor público do RustDesk pode ser usado para homologação com dados fictícios. O Gerenciador precisa cumprir a exigência de login do serviço público. Para operação da WolkUp, utilize uma implantação autorizada do RustDesk Server OSS com ponto acessível pela internet. Configure o servidor de ID, o relay e a chave pública nos dois aplicativos. O cliente atendido pode operar sem VPN. O uso de produção depende de validar o servidor escolhido, o acesso e a confiabilidade do relay.

## Teste em dois PCs

Use Windows 10 e Windows 11 x64 em redes independentes. Registre edição do Windows, versão, hash e resultado de cada cenário.

| Cenário | Evidência |
| --- | --- |
| Portátil e instalação | Os dois aplicativos iniciam. No Cliente instalado, confira bandeja, serviço, reinício, inicialização automática e desinstalação. |
| Autorização | O operador autorizado conecta. Uma conta fora do grupo falha e o Gerenciador rejeita sessões de entrada. O Cliente rejeita saídas. |
| Acesso assistido | O Cliente exige ação local. Recuse, aceite, encerre e confirme que o controle cessa. |
| Acesso não assistido | Tentativa com senha curta falha. Teste senha válida e incorreta e repita após revogar o acesso. |
| Internet | Confirme sessão entre duas redes e repita via relay. Interrompa a rede e observe reconexão e autorização. |
| Recursos | Verifique teclado, mouse, clipboard, transferência de arquivo com hash, dois monitores e prompt UAC. |
| Desempenho | Meça CPU e memória em repouso e durante cinco minutos de sessão. Registre resolução, quantidade de monitores e condição da rede. |

A compilação consulta o RustDesk 1.5.3 pelo commit fixado em `upstream/rustdesk.lock` e aplica `upstream/patches/windows-roles.patch`. O workflow registra os passos de geração de ponte Flutter, compilação e empacotamento. A atribuição e a licença AGPL-3.0 do RustDesk acompanham os artefatos de homologação.
