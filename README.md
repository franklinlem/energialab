# EnergiaLab — Projeto Integrador VI

**Demonstração publicada:** https://energialab.franklem.com

Aplicação web estática em português. Abra `index.html` no navegador: a simulação começa automaticamente. Não exige instalação, banco de dados, Node.js, PHP ou serviços externos.

## Publicar na Hostinger

1. Escolha o domínio ou subdomínio no hPanel e abra o Gerenciador de Arquivos.
2. Faça backup de uma página existente antes de substituí-la.
3. Envie `index.html` para a pasta pública do site (normalmente `public_html`). Também pode usar uma subpasta exclusiva, como `public_html/energia`.
4. Acesse o endereço correspondente pelo navegador.
5. Envie `sitemap.xml` para a raiz do site. O endereço já está configurado como `https://energialab.franklem.com/`; altere-o se publicar em outro domínio.

## Usar a simulação

- Cenários: lâmpada de 60 W e cargas de 1.000 W ou 1.500 W; todos são modelos sintéticos com fator de potência 1 por padrão.
- Configure potência, tensão, fator de potência, tarifa, variação aleatória, intervalo, velocidade virtual, falhas de entrega e tópico.
- Pause para gerar amostras manualmente. Reiniciar zera a sessão e mantém os parâmetros; quando ativa, gera a primeira amostra imediatamente.
- O gráfico guarda as últimas 120 amostras. Lacunas indicam mensagens perdidas. A tabela mostra as últimas 20.
- CSV/JSON exportam até 10.000 amostras. Logs guardam até 1.000 registros. O histórico é mantido somente em memória; recarregar a página inicia outra sessão.
- As métricas de corrente/potência representam a última mensagem recebida; energia e custo representam a sessão do dispositivo virtual, incluindo mensagens perdidas. A taxa de entrega cobre a sessão completa; a análise de desvio cobre as amostras recebidas retidas.

## Modelo matemático

Corrente nominal = potência nominal / (tensão × fator de potência).
Corrente RMS sintética = corrente nominal × (1 + sorteio uniforme entre −variação e +variação).
Potência estimada = tensão × corrente RMS × fator de potência.
Tempo de uma amostra = intervalo real configurado × velocidade virtual.
Energia incrementada (kWh) = potência (W) × tempo da amostra (s) / 3.600.000.
Custo estimado = energia total × tarifa atual.

Cada amostra representa um intervalo virtual completo, inclusive na geração manual. A pausa não acumula energia. A tarifa atual é aplicada ao total da sessão; não há faturamento por tarifas históricas. A tensão e o fator de potência são parâmetros, não leituras do SCT013. O painel emula o fluxo MQTT sem implementar pacotes de rede, broker real, QoS ou retransmissões. Não há medição analógica nem prova de teste físico. Limite de 5% é apenas uma comparação dos dados sintéticos.

Interface responsiva com tema claro/escuro, SVG nativo e exportação local. Sem dependências CDN. Créditos: desenvolvido para o Projeto Integrador VI de Franklin Martins e grupo.
