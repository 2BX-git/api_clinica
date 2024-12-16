# API Clínica

API RESTful para gerenciamento de clínica médica, incluindo agendamentos, profissionais e usuários.

## Requisitos

- PHP 7.4 ou superior
- MySQL 5.7 ou superior
- Composer
- SSL/TLS para produção

## Configuração para Produção

1. **Variáveis de Ambiente**
   - Copie o arquivo `.env.example` para `.env`
   - Configure todas as variáveis de ambiente:
     - Credenciais do banco de dados
     - Chave JWT secreta
     - URLs permitidas para CORS
     - Configurações SSL

2. **Banco de Dados**
   - Execute o script `database/schema.sql` para criar as tabelas
   - Configure SSL/TLS se necessário
   - Crie índices apropriados para melhor performance

3. **Segurança**
   - Altere a chave JWT para uma string segura e única
   - Configure CORS apropriadamente
   - Habilite SSL/TLS
   - Configure firewalls e regras de acesso

4. **Servidor Web**
   - Configure o servidor web (Apache/Nginx) para apontar para a pasta `/public`
   - Habilite mod_rewrite no Apache
   - Configure HTTPS
   - Ajuste limites de upload e timeouts se necessário

5. **PHP**
   - Ajuste `php.ini`:
     ```ini
     memory_limit = 256M
     upload_max_filesize = 10M
     post_max_size = 10M
     max_execution_time = 30
     ```

## Deploy em Nuvem

### AWS
1. Crie uma instância EC2 ou use Elastic Beanstalk
2. Configure o RDS para MySQL com SSL
3. Use Secrets Manager para variáveis de ambiente
4. Configure Load Balancer com SSL

### Google Cloud
1. Use App Engine ou Compute Engine
2. Configure Cloud SQL para MySQL
3. Use Secret Manager para variáveis
4. Configure SSL com Cloud Load Balancing

### DigitalOcean
1. Crie um Droplet ou use App Platform
2. Configure Managed Database
3. Use volumes para armazenamento persistente
4. Configure SSL com Let's Encrypt

## Checklist Pré-Deploy

- [ ] Todas as variáveis sensíveis estão no `.env`
- [ ] SSL/TLS está configurado
- [ ] Banco de dados está otimizado
- [ ] CORS está configurado corretamente
- [ ] Logs estão configurados
- [ ] Backups estão configurados
- [ ] Monitoramento está ativo

## Monitoramento

- Configure logs de erro
- Use ferramentas de monitoramento (New Relic, Datadog)
- Configure alertas para:
  - Erros 5xx
  - Tempo de resposta alto
  - Uso de CPU/memória
  - Espaço em disco

## Manutenção

- Faça backup regular do banco de dados
- Monitore logs de erro
- Atualize dependências regularmente
- Faça health checks periódicos
- Mantenha SSL/TLS atualizado

## Instalação

1. Clone o repositório para a pasta `htdocs` do XAMPP:
```bash
cd c:/xampp/htdocs
git clone [URL_DO_REPOSITORIO] api_clinica
```

2. Importe o banco de dados:
```bash
mysql -u root -p < database/schema.sql
```

3. Configure o arquivo `.env` com as credenciais do banco de dados:
```env
DB_HOST=localhost
DB_NAME=clinica
DB_USER=root
DB_PASS=
```

4. Acesse a API através do endereço:
```
http://localhost/api_clinica/public
```

## Autenticação

A API utiliza autenticação JWT (JSON Web Token). Para acessar as rotas protegidas, é necessário:

1. Fazer login através da rota `/auth/login`
2. Incluir o token retornado no header `Authorization` das requisições:
```
Authorization: Bearer [TOKEN]
```

## Rotas Disponíveis

### Autenticação
- `POST /auth/login` - Login de usuário

### Usuários (requer admin)
- `GET /usuarios` - Lista todos os usuários
- `POST /usuarios` - Cria um novo usuário
- `PUT /usuarios/{id}` - Atualiza um usuário
- `DELETE /usuarios/{id}` - Remove um usuário

### Clínicas
- `GET /clinicas` - Lista todas as clínicas
- `POST /clinicas` - Cria uma nova clínica (requer admin)

### Profissionais
- `GET /profissionais` - Lista todos os profissionais
- `POST /profissionais` - Cria um novo profissional (requer admin)
- `GET /profissionais/{id}/horarios-disponiveis` - Lista horários disponíveis do profissional

### Procedimentos
- `GET /procedimentos` - Lista todos os procedimentos
- `POST /procedimentos` - Cria um novo procedimento (requer admin)

### Especialidades
- `GET /especialidades` - Lista todas as especialidades
- `POST /especialidades` - Cria uma nova especialidade (requer admin)

### Agendamentos
- `GET /agendamentos` - Lista todos os agendamentos
- `POST /agendamentos` - Cria um novo agendamento
- `GET /agendamentos/{id}` - Busca um agendamento específico
- `POST /agendamentos/{id}/confirmar` - Confirma um agendamento
- `POST /agendamentos/{id}/cancelar` - Cancela um agendamento

## Documentação

A documentação completa da API está disponível em formato OpenAPI (Swagger) no arquivo `swagger.yaml`. Para visualizar:

1. Acesse [Swagger Editor](https://editor.swagger.io/)
2. Copie e cole o conteúdo do arquivo `swagger.yaml`

## Segurança

- Todas as rotas (exceto login) requerem autenticação via JWT
- Rotas administrativas requerem usuário com tipo "admin"
- Senhas são armazenadas com hash seguro
- Proteção contra SQL Injection usando PDO com prepared statements
- Validação de dados em todas as entradas

## Desenvolvimento

Para contribuir com o projeto:

1. Faça um fork do repositório
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Faça commit das alterações (`git commit -am 'Adiciona nova feature'`)
4. Faça push para a branch (`git push origin feature/nova-feature`)
5. Crie um Pull Request

## Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.
