# Gen certificates with CA

> Docs: 
https://mariadb.com/docs/server/security/data-in-transit-encryption/create-self-signed-certificates-keys-openssl/

```bash
openssl genrsa -out ca-key.pem 2048
```

```bash
openssl req \
  -days 3650 \
  -new -x509 \
  -key ca-key.pem \
  -out ca-cert.pem \
  -subj "/C=UA/ST=Denial/L=Springfield/O=Dis/CN=zabbix.example.com"
```

```bash
openssl req -newkey rsa:2048 -noenc -days 3650 \
   -keyout zabbix-agent-key.pem \
   -out zabbix-agent-req.pem \
   -subj "/C=UA/ST=Denial/L=Springfield/O=Dis/CN=zabbix.example.com"
```

```bash
openssl x509 -req -days 3650 -set_serial 01 \
   -in zabbix-agent-req.pem \
   -out zabbix-agent-cert.pem \
   -CA ca-cert.pem \
   -CAkey ca-key.pem \
   -subj "/C=UA/ST=Denial/L=Springfield/O=Dis/CN=zabbix.example.com"
```
