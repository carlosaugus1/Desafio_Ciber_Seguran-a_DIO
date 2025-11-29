Desafio: Testes de Força Bruta com Medusa
Sobre o Projeto
Esse projeto foi desenvolvido como parte do desafio do curso de Cibersegurança da DIO. O objetivo é entender como funcionam os ataques de força bruta e como podemos nos proteger deles em sistemas reais.​
- O que aprendi
Força bruta é quando um atacante tenta várias combinações de senha até acertar. Parece simples, mas é muito efetivo quando as pessoas usam senhas fracas como "123456" ou "password".​

- Ferramentas Utilizadas
Kali Linux: Sistema operacional para testes de segurança

Metasploitable 2: Máquina vulnerável feita de propósito para praticar​

Medusa: Ferramenta para testar senhas em vários serviços​

VirtualBox: Para rodar as máquinas virtuais

- Configuração do Ambiente
Configurei duas máquinas virtuais no VirtualBox com rede Host-Only para que elas conversem entre si sem afetar minha rede real.

Verificar conectividade:

bash
# Ver meu IP no Kali
ip addr

# Testar se consigo falar com o Metasploitable
ping 192.168.56.101
- Testes Realizados
Teste 1: Ataque ao FTP
O Metasploitable tem um servidor FTP rodando na porta 21. Criei uma lista pequena de senhas comuns e testei:​

bash
medusa -h 192.168.56.101 -u msfadmin -P senhas.txt -M ftp
O que cada parte faz:​

-h: IP da máquina alvo

-u: Nome do usuário (tentei com "msfadmin")

-P: Arquivo com as senhas para testar

-M: Tipo de serviço (ftp nesse caso)

Resultado: Consegui descobrir a senha porque ela estava na minha lista. Na vida real, isso seria muito perigoso.

Teste 2: Tentativa no SSH
Tentei fazer o mesmo no SSH (porta 22):

bash
medusa -h 192.168.56.101 -u root -P senhas.txt -M ssh -t 4
O -t 4 significa que usei 4 threads para ir mais rápido. Mas percebi que atacar SSH demora mais porque o serviço tem proteções melhores.​

- Minha wordlist (senhas.txt)
Criei uma lista bem básica para os testes:

text
admin
password
123456
msfadmin
root
user
Sei que existem listas gigantes tipo RockYou, mas para aprender achei melhor fazer uma pequena primeiro.

- Como se Proteger
Depois de fazer os testes, entendi porque essas práticas são importantes:

Usar senhas fortes: Nada de "123456" ou "password"

Bloquear após tentativas falhas: Depois de 3-5 erros, bloquear a conta por um tempo

Autenticação de dois fatores: Mesmo que descubram a senha, não conseguem entrar

Monitorar logs: Ficar de olho em tentativas suspeitas

Desabilitar serviços não usados: Se não precisa do FTP, desligue

- Reflexão
Achei interessante ver na prática como senhas fracas são um problema sério. Quando configurava servidores antes, não levava tanto a sério, mas agora vejo que qualquer um com o Kali pode fazer isso.​

O mais importante que aprendi: segurança não é só sobre ferramentas, é sobre boas práticas.

!!! Aviso Importante
Todos os testes foram feitos em ambiente controlado (VirtualBox com rede isolada). Nunca use essas técnicas em sistemas que você não tem autorização para testar!

-  Referências
Aulas do curso de Cibersegurança - DIO

Documentação da ferramenta Medusa

Guia do Metasploitable 2
