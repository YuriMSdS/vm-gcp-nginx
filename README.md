Neste projeto a nuvem utilizada será a GCP (google cloud plataform), o objetivo é criar uma VM e instalar o programa NGNIX.
  A máquina será criada com configurações básicas visando o baixo custo.
  
   Para criar a VM, no painel basta entrar no serviço chamado 'Compute Engine' e em seguida 'Instâncias de VM', após acessar, será necessário selecionar a opção 'Criar Instância'.
   
   Embora exista muitos parâmetros de criação de instância, neste projeto o objetivo é criar uma máquina de baixo custo, então a configuração será a seguinte:
    
    Nome: *opcional* (ex:Vm1)
    Região: *verificar melhor disponibilidade* (ex: Eastern US)
    Zona: *verificar melhor disponibilidade de acordo com a região* (ex: us-east1-c)
    Série: E2
    Tipo de máquina: 2vCPUs
    Disco de inicialização: Novo disco permanente equilibrado de 10 GB Imagem do SO: Debian GNU/Linux 11 (bullseye)
    Firewall: permitir Tráfego HTTP
 
 Vale destacar que também é possível criar utilizando o Cloud shell (basta clickar no ícone a esquerda do ícone de notificação do painel) e utilizar a seguinte linha:

 > gcloud compute instances create vm2 --machine-type e2-medium --zone us-east1-c

 A saída deve ser algo como:

    Created [...vm2].
     NAME: vm2
     ZONE: us-east1-c
     MACHINE_TYPE: e2-medium
     PREEMPTIBLE:
     INTERNAL_IP: 10.169.0.4 (exemplo)
     EXTERNAL_IP: 30.156.21.111 (exemplo)
     STATUS: RUNNING

 Utilizando o comando acima, ele criará uma VM nos idêntica a aquela criada no painel

   Após a criação da máquina (seja ela feita através do painel ou do cloud shell), na sessão de VMs, vai ter a instância criada, para realizar a instalação do NGINX, clique em SSH (irá inicializar o SSH no próprio navegador).

   uma vez acessado o SSH
      
 >atualize o SO.
     
    sudo apt-get update

 A saída esperada deve ser algo como:

     Get:1 http://security.debian.org stretch/updates InRelease [94.3 kB]
    Ign http://deb.debian.org strech InRelease
    Get:2 http://deb.debian.org strech-updates InRelease [91.0 kB]
    ...

>Agora instale o NGINX:

     sudo apt-get install -y nginx

A saída esperada é:

     Reading package lists… Done
    Building dependency tree
    Reading state information... Done
    The following additional packages will be installed:
    ...

>Agora Confirme se o NGINX está sendo executado

    ps auwx | grep nginx

Saída esperada:

    root      2330  0.0  0.0 159532  1628 ?        Ss   14:06   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
    www-data  2331  0.0  0.0 159864  3204 ?        S    14:06   0:00 nginx: worker process
    www-data  2332  0.0  0.0 159864  3204 ?        S    14:06   0:00 nginx: worker process
    root      2342  0.0  0.0  12780   988 pts/0    S+   14:07   0:00 grep nginx

 Agora basta testar, pegando o IP externo da VM e colocando no navegador, assim que pesquisar, aparecendo a página na web com "Welcome to NGINX!" significa que está tudo certo e já pode ser utilizado!

 [Legenda]

>sudo= executa a ação como superusuário (sem restrições)

>ps auwx | grep nginx= ele lista as ações mas somente relacionadas ao nginx

>tem outras formas de listar focando no nginx, sendo:

    Ps aux | grep nginx
    Systemctl status nginx
    Systemctl status service.nginx   