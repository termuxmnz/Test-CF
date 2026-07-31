'use strict';
const fs=require('fs');const path=require('path');const root=path.resolve(__dirname,'..');fs.copyFileSync(path.join(root,'data','db.seed.json'),path.join(root,'data','db.json'));console.log('Demonstração restaurada: estoque 4, sem pedidos e contas.');
