# Declaração de Saúde · Vida e Saúde

Formulário online da Declaração de Saúde dos titulares e dependentes da Vida e Saúde Assistência Médica (ANS nº 42.477-3).

## Arquivos

| Arquivo | O que é |
|---|---|
| `index.html` | Página do endereço raiz. Hoje: v1.2 (Amazon Copy). Na virada para produção da v2.0, passa a ser a v2.0 e mostra "peça o link ao RH". |
| `404.html` | v2.0. O GitHub Pages serve este arquivo para qualquer caminho que não existe, então é ele que atende os links por empresa (`/nome-codigo`). |
| `CNAME` | Domínio `declaracao.tenhavidaesaude.com.br`. |

## Links por empresa (v2.0)

Cada empresa recebe um link próprio no formato `declaracao.tenhavidaesaude.com.br/nome-da-empresa-xxxxx` (nome + código de 5 caracteres).

- A empresa vem do banco (`declaracao_saude.empresas`); cada declaração fica ligada a ela (`declaracoes.empresa_id`).
- Link desativado ou inexistente: a página avisa que o link não está ativo.
- Endereço sem código (a partir da produção da v2.0): a página pede o link ao RH da empresa.

Criar o link de uma empresa nova (SQL Editor do Supabase, projeto ERP ARASYS):

```sql
select declaracao_saude.criar_link_empresa('Nome da Empresa', '00.000.000/0001-00'); -- CNPJ opcional
```

Desativar um link: `update declaracao_saude.empresas set ativo = false where slug = '...';`

## Registro (respaldo contra fraude)

- Esquema `declaracao_saude`, fora da API pública; acesso só pela função.
- Tabelas `declaracoes`, `anexos`, `indicacoes_clinicas` e `envios_email` imutáveis: UPDATE, DELETE e TRUNCATE são bloqueados por gatilho.
- Cada registro guarda horário do servidor, IP, navegador, origem, empresa e o SHA-256 do conteúdo canônico (respostas, assinatura e documentos).
- Funções: `declaracao-saude` (v1.2, endereço raiz) e `declaracao-saude-v2` (v2.0, links por empresa).

## Publicar alterações

Edite `index.html` ou `404.html` e faça push na branch `main`. O GitHub Pages atualiza em cerca de 1 minuto.
