# 🎁 Sistema Win7 Med Presente — Publicação

Sistema **separado do JPR** para captação de leads via QR Code dos parceiros da Win7.

---

## ⚡ O que tem pronto

✅ Firebase já configurado (mesma conta `win7med-jpr`, coleção separada `presente_leads`)
✅ PIN do dashboard: **2026**
✅ Logo Win7 oficial embutido
✅ Form com campo "Quem te deu este presente?" + "Outros exames ou especialidade"
✅ Dashboard dedicado com filtro por parceiro indicador

---

## 🚀 Publicação em 3 passos (~10 minutos)

### Passo 1 — Liberar a coleção `presente_leads` no Firebase

1. Acesse: **https://console.firebase.google.com/project/win7med-jpr/firestore/rules**
2. Você verá as regras atuais. Substitua TUDO por:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /jpr_leads/{leadId} {
      allow read, create, update, delete: if true;
    }
    match /presente_leads/{leadId} {
      allow read, create, update, delete: if true;
    }
  }
}
```

3. Clique **"Publicar"** → **"Confirmar"**

> Isso libera AS DUAS coleções (JPR + Presente) sem mexer no que já funciona.

---

### Passo 2 — Criar repositório no GitHub

1. Vai em: **https://github.com/new**
2. **Repository name:** `win7med-presente`
3. **Public** ← marcar
4. NÃO marque outras opções
5. Clique **"Create repository"**

6. Na tela seguinte, clique em **"uploading an existing file"** (link azul)

7. **Arrasta** os arquivos da pasta `win7med-presente`:
   - `index.html`
   - `netlify.toml`

8. Embaixo, **"Commit changes"** (botão verde)

---

### Passo 3 — Publicar no Netlify

1. Vai em: **https://app.netlify.com/start**
2. Clica em **"Import from Git"** → **"Deploy with GitHub"**
3. Procura `win7med-presente` na lista → clica
4. Em **"Project name"** digita: `win7med-presente`
5. Build settings:
   - **Build command:** deixa **VAZIO**
   - **Publish directory:** **`.`** (um pontinho) ou vazio
6. Clica em **"Deploy win7med-presente"**

Em ~30 segundos vai estar no ar em:
**https://win7med-presente.netlify.app**

---

## 🎯 Como usar

### Para o lead (dono da clínica)
- Acessa: `https://win7med-presente.netlify.app`
- OU com indicador pré-preenchido: `https://win7med-presente.netlify.app/?indicacao=Dr.%20Carlos%20Mendes`
- Preenche o formulário e envia

### Para a Ranna (dashboard)
- Acessa: `https://win7med-presente.netlify.app/dashboard`
- Digita PIN: **2026**
- Vê todos os leads de presente em tempo real
- Filtra por parceiro indicador
- Exporta CSV

---

## 🔗 QR Codes para os parceiros

Para gerar QR Code de cada parceiro com nome pré-preenchido, use uma URL assim:

```
https://win7med-presente.netlify.app/?indicacao=NOME_DO_PARCEIRO
```

**Exemplos:**
- `https://win7med-presente.netlify.app/?indicacao=Dr.%20Carlos%20Mendes`
- `https://win7med-presente.netlify.app/?indicacao=Clinica%20Bem%20Estar`

> Espaços viram `%20` na URL. Use ferramentas tipo **qr-code-generator.com** para gerar o QR.

---

## 🔧 Troubleshooting

**Form mostra "Não foi possível enviar":**
- Verifique se as regras do Firestore (Passo 1) foram publicadas
- Abra console do navegador (F12) e veja erros

**Dashboard não mostra leads:**
- Confirme que está usando o PIN `2026`
- Confirme que as regras do Firestore foram atualizadas

**Quero mudar o PIN:**
- Edite `index.html` no GitHub → busca por `dashboardPin: "2026"` → muda → commit

**Quero adicionar mais parceiros como filtro no dashboard:**
- Não precisa! O filtro mostra automaticamente todos os indicadores que aparecerem nos leads salvos.

---

**Win7 Med · Presente · 2026** 🎁
