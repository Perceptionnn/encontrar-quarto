# Encontrar quartos em Almada ate 380 EUR

Pipeline local e seguro para procurar quartos individuais em Almada e zonas proximas.

## O que faz

- Pesquisa Idealista, OLX, BQuarto e resultados web portugueses.
- Filtra quartos ate `380 EUR`.
- Dá prioridade a Almada, Cova da Piedade, Pragal, Cacilhas, Laranjeiro, Feijo/Feijó e zonas proximas.
- Exclui anuncios incompatíveis ou suspeitos quando o texto permite detetar isso.
- Evita duplicados entre execucoes.
- Guarda resultados em CSV.
- Gera um resumo dos melhores anuncios.
- Prepara mensagens de contacto, mas nao envia nada.

## Primeira execucao no Windows

1. Copia a configuracao inicial:

```powershell
Copy-Item config.example.json config.json
```

2. Corre a pesquisa:

```powershell
.\run_daily.ps1
```

Os resultados ficam em:

- `data\quartos.csv`
- `data\latest_summary.md`
- `data\contact_drafts.md`

## Agendar pesquisa diaria

Para correr todos os dias as 09:00:

```powershell
.\install_daily_task.ps1 -Time "09:00"
```

Podes mudar a hora:

```powershell
.\install_daily_task.ps1 -Time "19:30"
```

## Regras de seguranca

O pipeline nunca envia mensagens, documentos ou pagamentos. Apenas prepara rascunhos.

Assinala anuncios com sinais de alerta, incluindo pedidos de caução/sinal antes de visita, texto pouco claro, falta de localizacao, preco estranho ou condicoes incompatíveis.

## Notas importantes

Sites como Facebook Marketplace, OLX e Idealista podem bloquear scraping ou mudar HTML. O pipeline foi feito para falhar de forma segura: se uma fonte bloquear, as restantes continuam.

Facebook Marketplace e grupos publicos normalmente exigem sessao iniciada e podem ter restricoes tecnicas/legais. Por isso esta versao nao automatiza login nem mensagens no Facebook. Os resultados web podem ainda apanhar paginas publicas indexadas.
