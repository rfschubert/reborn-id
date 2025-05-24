# Projeto Certidão Reborn 🍼

Sistema para geração de certificados oficiais fictícios para bebês reborn, incluindo Certidão de Nascimento e Carteirinha de Vacinação SUSBR.

![Exemplo de Certidão](image.png)

## 🎯 Objetivo
Permitir que mães de bebês reborn gerem documentos personalizados em PDF com aparência oficial, contendo observação de "sem validade legal".

## 🛠️ Stack Tecnológica
- React 18
- Shadcn/ui (Componentes estilizados)
- react-pdf/pdf-lib (Geração de PDFs)
- Docker
- Nixpack (Para deploy no Coolify)

## 📋 Checklist de Implementação

### Configuração Inicial
- [ ] Criar projeto React com Vite
- [ ] Instalar e configurar Shadcn/ui
- [ ] Adicionar Dockerfile e docker-compose.yml
- [ ] Criar arquivo Nixpack para deploy
- [ ] Configurar ESLint/Prettier

### Funcionalidades Principais
- [ ] Página de formulário com inputs:
  - Nome do bebê
  - Sexo (dropdown)
  - Nome dos pais
  - Data de nascimento (date picker)
  - Cidade (autocomplete)
  - Lista de vacinas (multi-select)
- [ ] Lógica de geração de PDFs:
  - Certidão de Nascimento (formato oficial brasileiro)
  - Carteirinha SUSBR (cores condicionais)
- [ ] Sistema de templates PDF com:
  - Arabescos decorativos
  - Campos dinâmicos
  - Observações legais

### Estilização
- [ ] Design da Certidão:
  - Fundo verde claro (#F0FFF0)
  - Padrão de arabescos em SVG
  - Fonte serifada (ex: Times New Roman)
- [ ] Design da Carteirinha:
  - Gradiente azul bebê/rosa pastel
  - Logo SUSBR destacado
  - Layout tipo cartão de saúde

### Configuração de Deploy
- [ ] Dockerfile:
  ```dockerfile
  FROM node:18-alpine
  WORKDIR /app
  COPY package*.json ./
  RUN npm ci
  COPY . .
  RUN npm run build
  CMD ["npm", "run", "preview"]
  ```
- [ ] docker-compose.yml:
  ```yaml
  version: '3'
  services:
    reborn-docs:
      build: .
      ports:
        - "5173:5173"
      environment:
        - NODE_ENV=production
  ```
- [ ] nixpack.yml:
  ```yaml
  services:
    web:
      build: .
      ports:
        - "80:5173"
      environment:
        - NODE_ENV=production
  ```

## 🚀 Como Executar

### Desenvolvimento Local
```bash
npm install
npm run dev
```

### Com Docker
```bash
docker-compose up --build
```

### Variáveis de Ambiente
Criar `.env`:
```env
VITE_APP_NAME="Certidão Reborn"
VITE_OFFICIAL_DISCLAIMER="Documento sem validade oficial"
```

## 📂 Estrutura de Arquivos
```
/src
├── assets/          # Imagens/SVGs
├── components/      # Componentes Shadcn
├── templates/       # Templates PDF
├── utils/           # Lógica de geração de PDFs
├── App.tsx
└── main.tsx
```

## 🖨️ Especificações Técnicas

### Certidão de Nascimento
- Formato A4 vertical
- Elementos obrigatórios:
  - Brasão municipal
  - Numeração fictícia (ex: SUSBR-2024-XXXX)
  - Campos alinhados em tabela
  - Selo holográfico simulado

### Carteirinha SUSBR
- Dimensões: 8.5cm x 5.4cm
- Elementos:
  - QR Code gerado dinamicamente
  - Lista de vacinas com datas
  - Foto opcional do bebê
  - Código de barras fictício

## 📌 Notas Importantes
1. Todos os PDFs devem incluir marca d'água discreta com texto "Documento Decorativo"
2. Implementar validação de campos obrigatórios
3. Opção de download conjunto (ZIP com ambos documentos)
4. Preview dos documentos antes de gerar PDF

## 📄 Licença
MIT License - Uso livre para fins não comerciais
