# Análise de Vulnerabilidades na Metasploitable 3
Este projeto tem como âmbito demonstrar a identificação e exploração de vulnerabilidades num ambiente controlado.

## 1 - Topologia do laboratório     

De forma a realizar o projeto foram utilizadas as seguintes ferramentas:
- VirtualBox com duas máquinas virtuais, ligadas em rede interna, sendo a máquina com Kali Linux a máquina atacante e a máquina Metasploitable 3 como alvo.
- Nmap de forma a fazer o reconhecimento da rede e das portas vulneráveis na máquina alvo.
- Metasploit para explorar as portas encontradas.

## 2 - Reconhecimento da rede

Primeiramente usei o Nmap de forma a encontrar a máquina alvo dentro da rede. Para tal, utilizei o seguinte comando:
```
nmap -sn 192.168.1.0/24
```

Após a execução do mesmo obtive o resultado abaixo:

<img width="661" height="156" alt="{45A3AF78-DDAC-4D5F-903F-02A6B38CA4E0}" src="https://github.com/user-attachments/assets/d2868a93-ea40-4cdc-a23f-5611cacf4e91" />

Foi encontrada uma máquina com o IP 192.168.1.10, que neste caso é a máquina alvo.
De seguida, procurei descobrir quais as portas abertas na maquina alvo. Para tal usei o comando abaixo:

```
nmap -sV -p- -v -T4 192.168.1.10
```
Após a execução do comando obtive o resultado abaixo, que evidenciou diversas portas abertas, entre as quais a porta FTP (21), com o serviço ProFTPD 1.3.5 exposto. Esta porta irá ser util pois irá ser através dela que iremos obter acesso á máquina alvo.

<img width="905" height="260" alt="{351DAEB7-32F7-4C4A-AA59-951805EA3E2C}" src="https://github.com/user-attachments/assets/d034d380-e686-45cb-8269-f9660ac57c76" />

## 3 - Exploração da vulnerabílidade encontrada

Após identificar a porta com a vulnerabilidade, executei um ataque com um exploit compativel com o serviço encontrado na porta 21, encontrado no Metasploitable. 

<img width="638" height="199" alt="{E021C70A-0A20-4C6D-A652-9CC4BF8236F1}" src="https://github.com/user-attachments/assets/2b1560db-9a91-44fa-8f93-1c7b8e6212a5" />

De forma a executar o ataque, tive de encontrar um diretório web que permitisse a escrita de ficheiros. O diretório `` /var/www/html `` permitia a escrita de ficheiros, ou seja, permitiu carregar um ficheiro e através dele ganhar acesso á máquina alvo.

<img width="760" height="505" alt="{DC9ECB2B-F287-4584-91FB-08D4DB73C518}" src="https://github.com/user-attachments/assets/9c824ec6-d41b-41cd-a1c6-c6d31fef16bd" />

De seguida, iniciei a interação com a máquina alvo, onde através da linha de comandos consegui ver os ficheiros guardados no servidor FTP.

<img width="513" height="336" alt="{98909284-7101-4A18-9C25-37853E71FC5B}" src="https://github.com/user-attachments/assets/b94d7d33-3f57-40e4-8cc0-634f9df305cb" />

