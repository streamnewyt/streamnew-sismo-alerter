# 🌍 StreamNew Sismo Alerter

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-Automated-blue.svg)
![Data Source](https://img.shields.io/badge/Data-USGS-orange.svg)

Este projeto é um **verificador automático de sismos fortes** (≥ 6.0 de magnitude), que consulta a API oficial do USGS a cada 15 minutos e envia notificações push via **Firebase Cloud Messaging (FCM)** para dispositivos inscritos no tópico `ALERTAS_SISMOS_FORTES`.

---

## ✨ Funcionalidades
- Consulta periódica (cron job) a cada 15 minutos.
- Busca sismos recentes com magnitude ≥ 6.0.
- Evita notificações duplicadas usando `last_quake_id.txt`.
- Envia alertas automáticos via FCM para usuários do aplicativo.
- Atualiza o repositório com o último ID de sismo detectado.

---

## ⚙️ Como funciona
1. O workflow `check_earthquakes.yml` é acionado:
   - Manualmente (`workflow_dispatch`) ou
   - Automaticamente a cada 15 minutos (`cron: */15 * * * *`).
2. Instala dependências (Google Cloud CLI, jq, curl, bc).
3. Autentica no Google Cloud usando a chave de serviço (`FCM_SERVICE_ACCOUNT_JSON`).
4. Consulta a API do USGS:
https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&minmagnitude=6.0&starttime= (earthquake.usgs.gov in Bing)<últimas 2h>&orderby=time

Código
5. Se houver sismo novo:
- Cria um JSON simples com título e corpo da notificação.
- Envia via FCM para o tópico `ALERTAS_SISMOS_FORTES`.
- Atualiza `last_quake_id.txt` no repositório.

---

## 📂 Estrutura
.github/workflows/check_earthquakes.yml   # Workflow principal
last_quake_id.txt                         # Registro do último sismo enviado

---

## 📜 Licença
Este projeto está licenciado sob a **MIT License** – uso livre, com créditos mantidos.

---

## ⚠️ Aviso
- Os dados são obtidos da API oficial do USGS.  
- Não há garantias de disponibilidade ou precisão absoluta.  
- Este projeto é apenas para fins de alerta e consulta.

---

## 🙌 Contribuições
Sugestões e melhorias são bem-vindas! Abra uma *issue* ou envie um *pull request*.
