## Attack Scenario

### Initial Access
- [x] RCE/Web Shell obtido com usuário `www-data`
- [x] Execução remota de comandos validada
- [x] Reverse shell estabelecida

---

### Persistence Simulation
- [x] Persistência via Cron criada em `/etc/cron.d/`
- [x] Persistência via SSH Key adicionada em `/root/.ssh/authorized_keys`
- [x] Persistência via Systemd criada em `/etc/systemd/system/`

---

### Threat Activity
- [x] Comandos suspeitos executados (`curl`, `wget`, `chmod`, `bash`)
- [x] Arquivos suspeitos criados em `/tmp`
- [x] Serviço malicioso habilitado com `systemctl enable`
- [x] Tentativa de reconexão persistente validada

---

## IoCs (Indicators of Compromise)

### Network IoCs
- [x] IP do atacante identificado
- [x] Portas utilizadas identificadas (4444/4445)
- [x] Conexões suspeitas registradas via `ss -antp`

---

### Host IoCs
- [x] Nome do serviço malicioso identificado (`sys-update.service`)
- [x] Caminho do arquivo persistente documentado
- [x] Hash do script/binário coletado
- [x] Chave SSH maliciosa identificada
- [x] Arquivos alterados registrados

---

### Authentication IoCs
- [x] Usuário comprometido identificado
- [x] Sessões ativas registradas
- [x] Histórico de login analisado com `last`

---

### Persistence IoCs
- [x] Cron persistence identificada
- [x] SSH authorized_keys persistence identificada
- [x] Systemd persistence identificada

---

### Process IoCs
- [x] PID malicioso identificado
- [x] Processo pai identificado
- [x] Linha de comando capturada via `auditd`

---

### Detection Context
- [ ] Regra Wazuh acionada
- [ ] Timestamp do alerta registrado
- [x] Técnica MITRE ATT&CK associada

---

## LEIA

Experiência Prática Validada: Como você não tem experiência formal em cibersegurança, deve focar em transformar seus laboratórios (como o LAB 34 que você está desenvolvendo) em "experiência de projeto" detalhada no LinkedIn.
