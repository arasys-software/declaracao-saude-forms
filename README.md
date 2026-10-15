# Declaração de Saúde · Vida e Saúde

Formulário online da Declaração de Saúde dos titulares e dependentes da Vida e Saúde Assistência Médica (ANS nº 42.477-3).

- Página estática única (`index.html`).
- Empresa da primeira versão: Amazon Copy (constante `EMPRESA` no código).
- Ao concluir, a declaração é registrada pela função `declaracao-saude` (Supabase, projeto ERP ARASYS) e o titular baixa uma cópia em PDF com protocolo, horário do servidor e código de verificação SHA-256.

## Registro (respaldo contra fraude)

- Esquema `declaracao_saude`, fora da API pública; acesso só pela função.
- Tabelas `declaracoes` e `indicacoes_clinicas` imutáveis: UPDATE, DELETE e TRUNCATE são bloqueados por gatilho.
- Cada registro guarda horário do servidor, IP, navegador, origem e o SHA-256 do conteúdo canônico das respostas.
- Origens aceitas pela função: `arasys-software.github.io`, `declaracao.tenhavidaesaude.com.br`, `tenhavidaesaude.com.br`.

## Ambientes

| Ambiente | Endereço |
|---|---|
| Teste | https://arasys-software.github.io/declaracao-saude-forms/ |
| Produção | declaracao.tenhavidaesaude.com.br (Hostinger) |

## Publicar alterações

Edite `index.html` e faça push na branch `main`. O GitHub Pages atualiza em cerca de 1 minuto.
