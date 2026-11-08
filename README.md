# CALMA | Consultoria em Aleitamento Materno (versão 1.0)

App web instalável no celular (PWA). Arquivos: `index.html` (o app inteiro, com a logo embutida), `manifest.webmanifest`, `sw.js`, ícones `icon-*.png` e `logo.png` (fundo transparente).

## Primeiro uso
O app começa vazio. Na primeira abertura, a consultora cria uma senha e preenche seus dados em Ajustes (nome e WhatsApp). Para conhecer o app antes, use "Explorar com dados de exemplo" e depois Ajustes → "Apagar dados fictícios e começar".

## Onde os dados ficam salvos
Tudo fica salvo no próprio celular, inclusive as fotos, e continua lá ao fechar o app ou desligar o aparelho. O app lembra de fazer backup toda semana: o arquivo vai pelo menu de compartilhar do celular para o Google Drive, iCloud ou e-mail. Para trocar de celular: instalar o app no aparelho novo e usar Ajustes → Restaurar.

## Como instalar
O app precisa estar num endereço https (ex.: GitHub Pages). No iPhone: abrir o endereço no Safari → Compartilhar → "Adicionar à Tela de Início". No Android: abrir no Chrome → menu ⋮ → "Instalar app". Depois disso ele abre pelo ícone, em tela cheia, e funciona sem internet.

## Navegação (5 abas)
Início · Clientes · Agenda · Atendimentos · Ajustes. O perfil da mãe é o centro: bebês, visitas, registros e fotos ficam ligados a ele.

## Fluxos do MVP
1. Cadastrar cliente (mãe + um ou mais bebês)
2. Gerar link de cadastro para a cliente (WhatsApp), com revisão e sem duplicar fichas (busca por cliente do link, CPF, e-mail e nome)
3. Perfil da cliente com linha do tempo (datas, descrições, fotos)
4. Agendar visita e ver na agenda (dia, semana, mês, com status)
5. Abrir a visita e tocar em "Registrar atendimento" (rascunho salvo automaticamente)
6. Fotos pela câmera ou galeria
7. Histórico geral na aba Atendimentos
8. PDF com logo e fotos para WhatsApp, ou e-mail

## Ficha da cliente
Dados da mãe, parceiro(a), gestação e saúde (DPP, pré-natal, nº de gestações/partos/abortos, pré-natalista, maternidade, pediatra, alergias, restrição alimentar, medicamentos, mamas na gestação), rede de apoio e bebês. Gestantes aparecem com a DPP; o bebê pode ter só o nome escolhido. O peso do bebê no registro é opcional.

## Para incluir novos campos
No `index.html`, edite `SECOES_MAE` e `CAMPOS_BEBE` (uma linha por campo). Formulário, ficha pública e perfil se ajustam sozinhos.

## Integrações externas (o que funciona hoje e o que precisa de servidor)
| Função | Hoje (sem servidor) | Versão completa |
|---|---|---|
| Login | Senha local no aparelho, bloqueio automático | Supabase Auth (e-mail e senha, 2FA) |
| Banco de dados | No celular (IndexedDB) + backup manual | Supabase Postgres com regras de acesso (RLS) |
| Fotos | Dentro do registro, no celular | Supabase Storage privado, links temporários |
| Agenda do celular | Arquivo .ics (iPhone) e link Google Agenda | Google Calendar API ou assinatura webcal |
| E-mail | Abre o app de e-mail com o resumo | Envio direto com PDF anexo (Resend/SendGrid) |
| PDF/WhatsApp | Gerado no celular, compartilhado pelo menu | Igual |
| Link de cadastro | Volta pelo WhatsApp como link de importação | Grava direto no banco, link individual de uso único |

## LGPD
Termo de consentimento no link de cadastro, data do aceite registrada na ficha, senha de acesso e bloqueio automático. Na versão com servidor: criptografia, registro de acessos, exclusão a pedido da titular.
