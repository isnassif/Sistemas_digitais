# Sistemas_digitais

Aqui está o texto unificado, consolidando as três etapas em uma narrativa lógica e técnica, formatado exatamente com as tags HTML que você utilizou:

<h2>Descrição do Projeto</h2> <p> Este projeto tem como objetivo a implementação de um <strong>coprocessador gráfico de alto desempenho</strong> para realizar, em tempo real, o redimensionamento de imagens (Zoom-In e Zoom-Out). O sistema foi desenvolvido utilizando o kit <strong>DE1-SoC</strong>, que integra uma FPGA Cyclone V e um Hard Processor System (HPS) baseado em ARM Cortex-A9. O coprocessador aplica técnicas de interpolação para variar o dimensionamento de imagens em escala de cinza (8 bits por pixel), exibindo o resultado via saída VGA. </p>

<div align="center"> <img src="https://www.rocketboards.org/foswiki/pub/Documentation/TerasicDE1SoCDevelopmentAndEducationBoard/igp_3e6715c483b2d44cc78aca35b032c4ef_DE1-SoC_top_s.jpg">


<strong>Imagem do Site da Altera</strong>



</div>

<section id="evolucao_tecnica"> <h2>Desenvolvimento e Arquitetura</h2> <p> O desenvolvimento foi estruturado em três etapas evolutivas, integrando progressivamente hardware e software para criar um sistema de vigilância e manipulação de imagem dinâmico: </p>

<ul> <li><strong>Etapa 1 (Fundação em Hardware):</strong> Implementação do núcleo do coprocessador na FPGA em Verilog. Nesta fase, o redimensionamento era controlado manualmente por chaves e botões físicos, com a imagem original carregada na memória via módulos do IP Catalog do Intel Quartus Prime Lite 23.1.</li>

<li><strong>Etapa 2 (Integração HPS-FPGA):</strong> Automação do controle através do processador ARM (HPS). Foi desenvolvida uma <strong>API em Assembly ARM</strong> que envia instruções diretamente à FPGA via ponte <strong>Avalon</strong>. Isso permitiu que o software controlasse os parâmetros de escala através de endereços mapeados em memória.</li>
</ul>

<div align="center"> <img src="diagramas/Captura de tela 2025-11-06 192558.png">


<strong>Diagrama do caminho de dados entre a API e o hardware.</strong>



</div>

<ul> <li><strong>Etapa 3 (Interação e Overlay):</strong> Finalização do sistema com foco em experiência do usuário. Foi implementada a interação via <strong>mouse USB</strong> e um software de controle em <strong>Linguagem C</strong>. A comunicação utiliza a ponte AXI Lightweight para enviar comandos de uma ISA customizada.</li> </ul> </section>

<section id="inovacao"> <h2>Diferenciais e Funcionalidades Finais</h2> <p> O sistema final consolidou-se como uma plataforma de <strong>zoom dinâmico</strong> com resposta instantânea. A principal inovação desta etapa final foi a introdução do <strong>Hardware Overlay</strong> para a geração do cursor e da área de seleção. </p> <p> Diferente de sistemas convencionais, o cursor e as bordas de seleção são injetados diretamente no pipeline de vídeo da FPGA. Isso elimina a necessidade de reescrever os dados da imagem na RAM a cada movimento do mouse, garantindo uma visualização limpa e processamento em tempo real sem sobrecarregar o barramento de memória. </p> <p> O usuário pode selecionar regiões específicas da imagem, realizar cortes e aplicar operações de ampliação ou redução, enquanto a controladora de hardware interpreta as instruções do HPS e ativa os módulos de processamento de imagem correspondentes. </p> </section>
