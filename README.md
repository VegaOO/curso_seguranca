# Estudos sobre Força Bruta, Medusa e Pós-Exploração
O repositório é uma forma de registrar tudo o que aprendi estudando ataques de força bruta, reconhecimento de serviços, conceitos de pós-exploração e o uso de ferramentas como Medusa, Nmap e alguns recursos do Metasploit.
Aqui minha ideia não é executar ataques reais, mas sim entender a lógica por trás das ferramentas e como elas são usadas em ambientes de teste e auditoria de segurança.

# O que entendi sobre ataques de força bruta
Em resumo, ataques de força bruta acontecem quando várias combinações de senha são testadas até alguma funcionar.

Aprendi que existem dois tipos principais:
> Força bruta tradicional: um usuário fixo + várias senhas.
> Password Spraying: várias contas + uma ou poucas senhas (muito usado quando muitas contas usam senhas fracas).

Percebi também que, apesar de parecer simples, esse é um dos ataques mais comuns quando um serviço está exposto sem proteção.

# Wordlist simples que estudei:
123456
admin
password
senha123
qwerty
toor

Mesmo pequena, uma lista dessas consegue quebrar muita coisa mal configurada.

# Entendendo o Medusa
Ao estudar o Medusa, percebi que ele é uma ferramenta poderosa e bem simples de usar para fazer ataques de força bruta em diversos serviços (FTP, HTTP, SMB, etc.).

O que achei mais interessante:
> Ele é rápido
> Usa múltiplas threads
> Trabalha com módulos diferentes para cada serviço
> A sintaxe é intuitiva

# Estrutura básica:
medusa -h <host> -u <usuario> -P <wordlist> -M <modulo>

# Exemplos teóricos que estudei:
# FTP: 
medusa -h 192.168.0.10 -u admin -P senhas.txt -M ftp

# Ataque em formulário web (DVWA, por exemplo):
medusa -h 192.168.0.10 -U users.txt -P senhas.txt -M web-form \
  -m FORM:"/login.php" \
  -m USERNAME:"username" \
  -m PASSWORD:"password" \
  -m DENY:"Login failed"

# Password Spraying em SMB:
medusa -h 192.168.0.10 -U usuarios.txt -P senha.txt -M smbnt

A partir desses comandos, consegui entender como a ferramenta realmente funciona, mesmo só estudando.

# Reconhecimento e Enumeração
Percebi que antes de pensar em tentar descobrir senhas, um atacante precisa primeiro descobrir o que existe no alvo.

Isso inclui:
> portas abertas
> versões dos serviços
> protocolos que podem ter falhas

Ferramentas que estudei:
> nmap
> enum4linux
> whatweb

# Exemplo de comando Nmap que eu analisei:
nmap -sV -p- 192.168.0.10
Com isso, já dá pra ter uma boa noção do cenário e onde focar os testes.

# Conceito de Pós-Exploração
Depois de estudar essa parte, entendi que a pós-exploração começa quando você já conseguiu algum acesso.
É o momento em que o atacante tenta:

> elevar privilégios
> extrair informações
> manter persistência
> se mover lateralmente para outras máquinas

Exemplos de comandos que aprendi do Meterpreter:

Baixar arquivos:
download arquivo.txt

Migrar para outro processo:
migrate <PID>

Listar processos:
ps

Esses conceitos me ajudaram a entender como funciona o ciclo completo de um ataque.

# Reflexões Pessoais
Algumas coisas que percebi enquanto estudava:

> Muitas vulnerabilidades surgem simplesmente por senhas fracas.
> Protocolos antigos (como FTP e Telnet) ainda são usados, e isso abre brechas enormes.
> As ferramentas são muito poderosas, mas também deixam claro como a segurança depende mais de configuração do que de ferramentas.
> Uma boa política de bloqueio e autenticação multifator já elimina grande parte desses ataques.
> Segurança é basicamente estar sempre um passo à frente.

# Mitigações que estudei

# Em FTP:
> desativar login anônimo
> usar SFTP ou FTPS
> limitar tentativas

# Em formulários web:
> captcha
> MFA
> rate limiting
> bloquear IPs suspeitos

# Em SMB:
> desativar SMBv1
> reforçar políticas de senha
> restringir compartilhamentos

# Conclusão

Organizar esses estudos me ajudou a entender muito melhor como um ataque funciona desde o começo até a pós-exploração.
Mesmo sem executar nada fora de um contexto controlado, já dá pra perceber como os conceitos se encaixam e como um ambiente mal configurado pode ser facilmente comprometido.

Esse repositório é basicamente o registro da minha jornada de aprendizado, dos comandos que estudei e das conclusões que fui tirando ao longo do processo.
