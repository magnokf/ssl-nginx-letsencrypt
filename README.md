# ssl-nginx-letsencrypt

# Configuração de Certificados SSL com Let's Encrypt e Nginx

Este documento detalha o processo de instalação e configuração de certificados SSL no servidor Nginx, utilizando o Let's Encrypt como Autoridade Certificadora (CA). O processo é automatizado pelo Certbot, facilitando a obtenção e a renovação dos certificados.

## Pré-requisitos

- Um servidor rodando Ubuntu ou outra distribuição Linux compatível.
- Acesso sudo ao servidor.
- Nginx instalado e configurado para servir ao menos um domínio.
- Um nome de domínio configurado para apontar para o IP do servidor.

## Passo 1: Instalação do Certbot

1. **Atualizar os Pacotes do Sistema**:
   Assegure-se de que todos os pacotes do sistema estão atualizados:
   ```bash
   sudo apt update
   sudo apt install certbot python3-certbot-nginx
   ```

## Passo 2: Obtenção e Configuração de Certificados SSL
Execute o Certbot para automatizar a configuração dos certificados SSL com o Nginx:
```bash
sudo certbot --nginx
```
Durante o processo, você será solicitado a:

Fornecer um endereço de e-mail para notificações de segurança.
Aceitar os Termos de Serviço.
Optar pelo redirecionamento automático de HTTP para HTTPS (recomendado).
O Certbot tentará validar seu domínio via desafio HTTP, garantindo que você tenha autoridade sobre o mesmo.

## Passo 3: Verificação e Recarregamento do Nginx
Verifique se a configuração do Nginx está correta e livre de erros:
```bash
sudo nginx -t
```
Se o teste for bem-sucedido, recarregue o serviço para aplicar as configurações:
```bash
sudo systemctl reload nginx
```

## Passo 4: Renovação Automática
Certbot configura automaticamente um cron job ou systemd timer para renovação dos certificados. Para verificar se o timer está ativo:
```bash
sudo systemctl list-timers | grep certbot
```




