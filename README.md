Code Forge Pedidos — demonstração full-stack
Sistema demonstrativo de pedidos para Code Forge Restaurante e Code Forge Lanches, com cardápio separado, adicionais, cálculo no servidor, estoque, conta de cliente, painel administrativo, acompanhamento de status e finalização pelo WhatsApp.
O que funciona
escolha destacada entre Restaurante e Lanches;
categorias independentes dentro de cada operação;
oito produtos reais de demonstração com fotos e preços;
adicionais obrigatórios e opcionais;
limite mínimo e máximo de escolhas;
opções exclusivas, como “sem vegetais” e “sem molhos”;
campo universal de observação;
carrinho e checkout;
retirada ou entrega;
taxa de entrega calculada no servidor;
preços recalculados no back-end;
estoque inicial de 4 unidades por produto;
produto cinza e indisponível quando o estoque chega a zero;
prevenção de pedido duplicado por chave de idempotência;
pedido salvo antes de abrir o WhatsApp;
código único de pedido;
cadastro e login opcional do cliente;
histórico de pedidos da conta;
painel com pedidos, status, preços, estoque e abertura/fechamento;
cancelamento com devolução automática do estoque;
página de acompanhamento;
restauração completa da demonstração.
Como iniciar
É necessário ter o Node.js 20 ou superior.
Extraia o ZIP.
Abra um terminal dentro da pasta.
Execute:
```bash
npm start
```
Abra:
```text
http://localhost:3000
```
O projeto usa apenas recursos nativos do Node.js. Não existe `npm install` porque nenhuma biblioteca externa é necessária.
Painel administrativo
Endereço:
```text
http://localhost:3000/admin.html
```
Credenciais da demonstração:
```text
E-mail: admin@codeforge.test
Senha: CodeForge@2026
```
Essas credenciais são públicas apenas para facilitar o teste. Em produção, use as variáveis `ADMIN_EMAIL` e `ADMIN_PASSWORD`.
Teste principal de estoque
Todos os produtos começam com 4 unidades.
Escolha um produto.
Adicione 4 unidades.
Finalize o pedido.
O servidor reduz o estoque para zero.
Ao voltar ao cardápio, o produto aparece cinza e com a marca “Indisponível”.
No painel, você pode repor o estoque ou cancelar o pedido para devolver as unidades.
WhatsApp
O servidor salva o pedido e o valor oficial no painel antes de abrir o WhatsApp. A mensagem leva produtos, adicionais, observações, subtotal, taxa e total.
Nesta demonstração, o site usa `wa.me`, portanto o cliente ainda precisa pressionar “Enviar” e tecnicamente pode editar a mensagem. Isso não altera o pedido salvo no painel.
Envio totalmente automático exige a WhatsApp Business Platform/Cloud API, um número empresarial configurado e credenciais secretas no back-end. Veja `PRODUCAO.md`.
Segurança implementada no teste
preços e adicionais validados no servidor;
estoque validado e reduzido no servidor;
idempotência para não reduzir o estoque duas vezes;
gravação serializada e atômica do banco JSON;
cookies `HttpOnly` e `SameSite=Strict`;
senha de cliente com PBKDF2 e salt individual;
painel protegido por sessão;
token CSRF nas alterações administrativas;
limitação básica de tentativas por IP;
limites de tamanho e sanitização de entradas;
Content Security Policy e cabeçalhos de segurança;
proteção contra acesso fora da pasta pública.
Limitações honestas
O banco desta versão é um arquivo JSON e as sessões ficam na memória do processo. É adequado para apresentação, aprendizado e demonstração local, mas não é a arquitetura final recomendada para clientes reais.
Em produção, migre para Supabase/PostgreSQL, autenticação gerenciada, backups, logs, monitoramento e HTTPS. O esquema inicial está em `production/supabase-schema.sql`.
Estrutura
```text
server.js                    back-end e API
public/index.html            cardápio e checkout
public/app.js                cliente, carrinho, adicionais e conta
public/admin.html            painel administrativo
public/admin.js              pedidos, status, produtos e estoque
public/acompanhar.html       rastreamento do pedido
data/db.json                 banco atual da demonstração
data/db.seed.json            estado original para restauração
production/supabase-schema.sql  base sugerida de produção
```
Abrir no celular na mesma rede
No Windows, execute `ipconfig`, encontre o endereço IPv4 do computador e abra no celular:
```text
http://SEU-IP:3000
```
O computador e o celular precisam estar na mesma rede Wi-Fi. O firewall do Windows pode solicitar permissão para o Node.js.
