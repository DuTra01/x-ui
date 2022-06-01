# x-ui

Painel de xRay com suporte multiusuário multiprotocolo

# Características

- Monitoramento do estado do sistema
- Suporte multi-protocolo multiusuário, operação de visualização de página da web
- Protocolos suportados: vmess, vless, trojan, shadowsocks, dokodemo-door, socks, http
- Suporte para configurar mais configurações de transmissão
- Estatísticas de tráfego, limite de tráfego, limite de tempo de expiração
- Modelos de configuração de raio x personalizáveis
- Suporte ao painel de acesso https (traga seu próprio nome de domínio + certificado ssl)
- Suporte a aplicação de certificado SSL com um clique e renovação automática
- Para itens de configuração mais avançados, consulte o painel para obter detalhes

# Como instalar

```
bash <(curl -Ls https://raw.githubusercontent.com/DuTra01/x-ui/main/install.sh)
```

## Instalação manual

1. Primeiro de https://github.com/dutra01/x-ui/releases Baixe o pacote compactado mais recente，escolha geral `amd64`Arquitetura
2. Em seguida, faça o upload do pacote compactado para o servidor `/root/`diretório e use `root`servidor de login do usuário

> Se a arquitetura da CPU do seu servidor não for `amd64`，no comando `amd64`Substituir por outro esquema

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## Instalar usando o docker

> Este tutorial do docker e a imagem do docker são fornecidos por [Chasing66](https://github.com/Chasing66)

1. Instalar janela de encaixe

```shell
curl -fsSL https://get.docker.com | sh
```

2. Instalar x-ui

```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
    -v $PWD/db/:/etc/x-ui/ \
    -v $PWD/cert/:/root/cert/ \
    --name x-ui --restart=unless-stopped \
    enwaiax/x-ui:latest
```

> Build 自己的镜像

```shell
docker build -t x-ui .
```

## Aplicativo de certificado SSL

> Esta função e tutorial são fornecidos por [FranzKafkaYu](https://github.com/FranzKafkaYu)

O script tem uma função de aplicativo de certificado SSL integrada. Para usar este script para solicitar um certificado, as seguintes condições devem ser atendidas:

- Conheça o endereço de e-mail registrado na Cloudflare
- Conheça a chave de API global da Cloudflare
- O nome de domínio foi resolvido para o servidor atual por meio do cloudflare

Como obter a chave de API global da Cloudflare:
    ![](media/bda84fbc2ede834deaba1c173a932223.png)
    ![](media/d13ffd6a73f938d1037d0708e31433bf.png)

Ao usar, basta digitar `domain name`, `email`, `API KEY`, o diagrama é o seguinte:
        ![](media/2022-04-04_141259.png)

Precauções:

- O script usa a API DNS para solicitação de certificado
- Use Let'sEncrypt como a parte CA por padrão
- O diretório de instalação do certificado é o diretório /root/cert
- Os certificados solicitados por este script são todos os certificados de nome de domínio genérico

## Uso do robô Tg (em desenvolvimento, temporariamente indisponível)

> Esta função e tutorial são fornecidos por [FranzKafkaYu](https://github.com/FranzKafkaYu)

X-UI suporta notificação diária de tráfego, lembrete de login do painel e outras funções através do robô Tg. Para usar o robô Tg, você precisa se inscrever por conta própria
Para tutoriais de aplicativos específicos, consulte [link do blog](https://coderfan.net/how-to-use-telegram-bot-to-alarm-you-when-someone-login-into-your-vps.html )
Instruções de uso: Defina os parâmetros relacionados ao robô no fundo do painel, incluindo

- Token de Robô Tg
- Tg Robot ChatId
- Tempo de execução do ciclo do robô Tg, na sintaxe do crontab

Sintaxe de referência:

- 30 * * * * * //Notificar aos 30s de cada ponto
- @hourly // notificações de hora em hora
- @daily // Notificação diária (00:00 AM)
- @every 8h // Notificação a cada 8 horas

Conteúdo da notificação TG:

- Uso de tráfego de nós
- Lembrete de login do painel
- Lembrete de expiração do nó
- Lembrete de aviso de trânsito

Mais recursos estão planejados...
## Sistema de sugestões

- CentOS 7+
- Ubuntu 16+
- Debian 8+

# Problema comum

## Migrando da v2-ui

Primeiro instale a versão mais recente do x-ui no servidor onde o v2-ui está instalado e, em seguida, use o seguinte comando para migrar, que migrará `todos os dados da conta de entrada` do v2-ui local para o x-ui, `painel configurações e nome de usuário e senha não serão migrados`

> Após a migração ser bem sucedida, por favor `feche v2-ui` e `restart x-ui`, caso contrário a entrada de v2-ui causará um `conflito de porta` com a entrada de x-ui
> 
```
x-ui v2-ui
```

## Problema encerrado

Todos os tipos de problemas brancos veem pressão alta

## Stargazers over time

[![Stargazers over time](https://starchart.cc/vaxilu/x-ui.svg)](https://starchart.cc/vaxilu/x-ui)
