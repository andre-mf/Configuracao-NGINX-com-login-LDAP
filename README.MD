### Para acessar o PHP LDAP Admin em http://localhost:8080, utilizar a credencial:

> **Login DN:** cn=admin,dc=example,dc=org
>
> **Password:** admin

### Para gerar os certificados usados no modo SSL, basta seguir os passos abaixo:

1. **Criar uma Autoridade Certificadora (CA)**

   Primeiro, criaremos uma CA que será usada para assinar os certificados do servidor e dos clientes.

    1. **Gerar a chave privada da CA:**

       ```shell
       openssl genpkey -algorithm RSA -out ca.key -aes256  
       ```
    2. **Criar o certificado da CA:**

       ```shell
       openssl req -x509 -new -nodes -key ca.key -sha256 -days 3650 -out ca.crt  
       ```

       Você será solicitado a fornecer algumas informações sobre a CA.

2. **Criar o certificado do servidor**

    1. **Gerar a chave privada do servidor:**

       ```shell
       openssl genpkey -algorithm RSA -out server.key  
       ```
    2. **Gerar um CSR (Certificate Signing Request) para o servidor:**

       ```shell
       openssl req -new -key server.key -out server.csr  
       ```
    3. **Assinar o CSR do servidor com a CA para obter o certificado do servidor:**

       ```shell
       openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out server.crt -days 365 -sha256  
       ```