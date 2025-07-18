# EAN/GTIN Finder Automático para Cosmos Bluesoft

Este projeto automatiza a busca de códigos de barras (EAN/GTIN) de produtos no site cosmos.bluesoft.com.br, preenchendo automaticamente a coluna BARCODE em arquivos CSV de produtos.

Repositório oficial: [https://github.com/sidnei-almeida/ean_code_finder](https://github.com/sidnei-almeida/ean_code_finder)

## 🚀 Funcionalidades
- Busca automática do código EAN/GTIN de cada produto usando o campo de busca do Cosmos Bluesoft.
- Atualiza/cria a coluna `BARCODE` em cada CSV processado.
- Suporte a múltiplos arquivos CSV na pasta `dados/`.
- Detecção automática do Cloudflare durante o processo, com instruções claras para o usuário.
- Log detalhado do processo em `processar_dados.log`.

## ⚙️ Requisitos
- **Python 3.13** (ou superior)
- **Google Chrome** ou **Mozilla Firefox** instalado
- **pip** para instalar dependências

## 📦 Instalação
1. Clone o repositório:
   ```bash
   git clone https://github.com/sidnei-almeida/ean_code_finder.git
   cd ean_code_finder
   ```
2. Crie e ative um ambiente virtual (opcional, mas recomendado):
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   # ou
   venv\Scripts\activate  # Windows
   ```
3. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```

> **Não é mais necessário baixar o ChromeDriver ou GeckoDriver manualmente!**
> O script usa o [webdriver-manager](https://github.com/SergeyPirogov/webdriver_manager) para instalar e gerenciar o driver automaticamente, tanto no Windows quanto no Linux ou Mac.

## 📂 Como preparar os dados
1. Crie uma pasta chamada `dados` na raiz do projeto (se ainda não existir).
2. Coloque todos os arquivos `.csv` que deseja processar dentro da pasta `dados/`.
3. Cada CSV deve ter uma coluna chamada `NOME` ou `nome` com o nome dos produtos.

## 🏃‍♂️ Como rodar o script
1. Execute o script principal:
   ```bash
   python processar_dados.py
   ```
2. O script tentará abrir o Google Chrome automaticamente. Se não encontrar, tentará o Mozilla Firefox.
   - Certifique-se de ter pelo menos um desses navegadores instalado.
   - O driver será baixado automaticamente na primeira execução.
3. **Leia com atenção o aviso no terminal!**
   - Assim que o navegador abrir, **passe manualmente pela verificação do Cloudflare** (página "Um momento..." ou "Checking your browser...").
   - **Só aperte ENTER no terminal depois que o site estiver totalmente carregado e a barra de busca aparecer.**
   - **NÃO feche o navegador enquanto o script estiver rodando!**
4. O script vai processar todos os CSVs na pasta `dados/`, preenchendo a coluna `BARCODE` com o código encontrado para cada produto.
5. **Se o Cloudflare aparecer novamente durante o processo:**
   - O script vai pausar automaticamente e mostrar um aviso super chamativo.
   - Resolva o Cloudflare manualmente no navegador e só então aperte ENTER no terminal para continuar.
   - Pode demorar alguns segundos para o script continuar após o ENTER.
6. **Se alguns produtos não encontrarem código de barras:**
   - Isso é normal e geralmente é culpa do Cloudflare.
   - Você pode rodar o script novamente só com esses produtos em um novo CSV para tentar buscar os códigos que faltaram.

## 📝 Exemplo de CSV de entrada
```csv
NOME
Coca-Cola 2L
Arroz Branco Tipo 1 5kg
Leite Integral 1L
```

## 🗂️ Saída
- Os arquivos CSV originais na pasta `dados/` serão atualizados com a coluna `BARCODE` preenchida.
- Um log detalhado será salvo em `processar_dados.log`.

## 💡 Dicas importantes
- **Compatível com Windows, Linux e Mac!**
- **Tenha paciência!** O Cloudflare pode aparecer mais de uma vez durante o processo.
- **Às vezes o Cloudflare entra em um loop de carregamento infinito** (fica só "carregando" e não aparece a caixinha para clicar). Isso é normal e acontece por proteção do site. **Nesses casos, espere alguns minutos sem fechar a página**: normalmente, depois de um tempo, o Cloudflare libera e a caixinha volta a aparecer para você clicar. 
- **Vale a pena tentar apertar F5 (atualizar a página)** para ver se o Cloudflare libera, mas **NUNCA feche a página do navegador** enquanto o script estiver rodando! Se fechar, o script vai perder a conexão com o navegador e dará erro.
- **Nunca feche o navegador enquanto o script estiver rodando.**
- Se o script for interrompido, você pode rodar novamente apenas com os produtos que faltaram.
- O tempo de espera entre buscas e pausas periódicas são essenciais para evitar bloqueios.

## ❓ Dúvidas ou problemas?
Se tiver qualquer dúvida, problema ou sugestão, abra uma issue ou entre em contato pelo [repositório no GitHub](https://github.com/sidnei-almeida/ean_code_finder).

---

Feito com ❤️ para automação de catálogos de produtos! 