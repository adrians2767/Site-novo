# site-das-plantas

<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Site das plantas</title>
    <style>
        /* =========================================
           PALETA DE CORES E VARIAVEIS
           ========================================= */
        :root {
            --verde-escuro: #2E5C31;
            --verde-claro: #4CAF50;
            --verde-fundo: #E8F5E9;
            --terra: #8D6E63;
            --laranja: #FF9800;
            --laranja-hover: #F57C00;
            --texto-escuro: #333333;
            --branco: #FFFFFF;
        }

        /* =========================================
           ESTILOS GERAIS (RESET)
           ========================================= */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--verde-fundo);
            color: var(--texto-escuro);
            line-height: 1.6;
        }

        /* =========================================
           CABEÇALHO
           ========================================= */
        header {
            background-color: var(--verde-escuro);
            color: var(--branco);
            text-align: center;
            padding: 3rem 1rem;
            border-bottom: 5px solid var(--laranja);
        }

        header h1 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
        }

        header p {
            font-size: 1.1rem;
            max-width: 800px;
            margin: 0 auto;
            color: #DDEEDD;
        }

        /* =========================================
           MENU INTERATIVO
           ========================================= */
        .menu-container {
            display: flex;
            justify-content: center;
            gap: 1rem;
            padding: 2rem 1rem;
            flex-wrap: wrap;
        }

        .btn-planta {
            background-color: var(--verde-claro);
            color: var(--branco);
            border: none;
            padding: 10px 20px;
            font-size: 1.1rem;
            font-weight: bold;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .btn-planta:hover, .btn-planta.ativo {
            background-color: var(--laranja);
            transform: translateY(-2px);
        }

        /* =========================================
           CONTEÚDO DINÂMICO (CARDS)
           ========================================= */
        main {
            max-width: 1000px;
            margin: 0 auto;
            padding: 0 1rem 3rem 1rem;
        }

        .titulo-secao {
            text-align: center;
            margin-bottom: 2rem;
            color: var(--verde-escuro);
            font-size: 2rem;
        }

        .grid-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 1.5rem;
        }

        .card {
            background-color: var(--branco);
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            border-top: 4px solid var(--terra);
            transition: transform 0.3s ease;
            opacity: 0;
            animation: fadeIn 0.5s forwards;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 6px 15px rgba(0,0,0,0.1);
        }

        .card h3 {
            color: var(--laranja-hover);
            margin-bottom: 0.5rem;
            font-size: 1.3rem;
        }

        .card p {
            color: #555;
            font-size: 0.95rem;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

    </style>
</head>
<body>

    <header>
        <h1>Descobrindo os Cultivares</h1>
        <p><strong>O que é uma cultivar?</strong> É uma variedade de planta que foi selecionada e cultivada pelo ser humano para destacar características específicas, como cor, tamanho, sabor ou resistência a pragas. Elas são a base da nossa alimentação e da agricultura moderna!</p>
    </header>

    <nav class="menu-container" id="menu-plantas">
        <button class="btn-planta ativo" data-planta="alface">Alface</button>
        <button class="btn-planta" data-planta="tomate">Tomate</button>
        <button class="btn-planta" data-planta="cenoura">Cenoura</button>
        <button class="btn-planta" data-planta="espinafre">Espinafre</button>
    </nav>

    <main>
        <h2 class="titulo-secao" id="titulo-planta">Cultivares de Alface</h2>
        <div class="grid-cards" id="container-cards">
            <!-- Cards injetados via JS -->
        </div>
    </main>

    <script>
        /* Banco de Dados das Plantas */
        const dadosCultivares = {
            alface: {
                titulo: "Cultivares de Alface",
                cultivares: [
                    { nome: "Crespa", descricao: "A mais consumida no Brasil. Possui folhas soltas, onduladas e não forma cabeça. Excelente para saladas volumosas." },
                    { nome: "Romana", descricao: "Folhas alongadas, duras e com nervuras claras. Muito crocante, é a estrela da clássica salada Caesar." },
                    { nome: "Mimosa", descricao: "Parecida com folhas de carvalho, possui recortes profundos e é muito delicada, com textura macia." },
                    { nome: "Americana", descricao: "Forma uma cabeça fechada como um repolho. É muito crocante e resiste bem a temperaturas mais altas." }
                ]
            },
            tomate: {
                titulo: "Cultivares de Tomate",
                cultivares: [
                    { nome: "Cereja", descricao: "Pequenos, redondos e bem adocicados. Perfeitos para aperitivos, espetinhos e saladas coloridas." },
                    { nome: "Carmem", descricao: "Conhecido como tomate longa-vida. Tem boa durabilidade e é ótimo para saladas do dia a dia." },
                    { nome: "Italiano", descricao: "Formato alongado e menos água em seu interior. É o favorito absoluto para fazer molhos encorpados." }
                ]
            },
            cenoura: {
                titulo: "Cultivares de Cenoura",
                cultivares: [
                    { nome: "Nantes", descricao: "Formato cilíndrico e ponta arredondada. Possui sabor doce e textura excelente, ideal para consumo cru." },
                    { nome: "Brasília", descricao: "Cultivar desenvolvida no Brasil, muito resistente ao calor do verão tropical. Ótima produtividade." },
                    { nome: "Baby", descricao: "Colhidas precocemente ou de cultivares específicas em miniatura. São extremamente macias e doces." }
                ]
            },
            espinafre: {
                titulo: "Cultivares de Espinafre",
                cultivares: [
                    { nome: "Verdadeiro", descricao: "Folhas lisas ou crespas, formato ovalado. Prefere climas mais amenos e frios." },
                    { nome: "Nova Zelândia", descricao: "Folhas mais grossas e em formato de flecha. Muito resistente ao calor, espalha-se como uma trepadeira." }
                ]
            }
        };

        const botoes = document.querySelectorAll('.btn-planta');
        const containerCards = document.getElementById('container-cards');
        const tituloPlanta = document.getElementById('titulo-planta');

        function renderizarCards(plantaKey) {
            containerCards.innerHTML = '';
            const dados = dadosCultivares[plantaKey];
            tituloPlanta.textContent = dados.titulo;

            dados.cultivares.forEach((cultivar, index) => {
                const card = document.createElement('div');
                card.className = 'card';
                card.style.animationDelay = `${index * 0.1}s`;
                
                card.innerHTML = `
                    <h3>${cultivar.nome}</h3>
                    <p>${cultivar.descricao}</p>
                `;
                
                containerCards.appendChild(card);
            });
        }

        botoes.forEach(botao => {
            botao.addEventListener('click', () => {
                botoes.forEach(b => b.classList.remove('ativo'));
                botao.classList.add('ativo');
                const plantaSelecionada = botao.getAttribute('data-planta');
                renderizarCards(plantaSelecionada);
            });
        });

        // Inicia com a primeira planta
        renderizarCards('alface');
    </script>
</body>
</html>
