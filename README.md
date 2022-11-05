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

 Utilizando o comando acima, ele criará uma VM nos idêntica a aquela criada no painel

   Após a criação da máquina (seja ela feita através do painel ou do cloud shell), na sessão de VMs, vai ter a instância criada, para realizar a instalação do NGINX, clique em SSH (irá inicializar o SSH no próprio navegador).

   >uma vez acessado o SSH
      
 >atualize o SO.
    sudo apt-get update
 A saída esperada deve ser algo como:
     Get:1 http://security.debian.org stretch/updates InRelease [94.3 kB]
    Ign http://deb.debian.org strech InRelease
    Get:2 http://deb.debian.org strech-updates InRelease [91.0 kB]
    ...