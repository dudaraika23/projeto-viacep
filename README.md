# Projeto Consulta de CEP - ViaCEP

## Integrantes:
- Ingrid Lara A. de Souza; 
- Maria Eduarda Raika S. Silva;
- Maria Eduarda Scardoelli.

## Sobre o Projeto:
O projeto realiza consulta de CEPs utilizando a API pública do ViaCEP.

## Teste da API no Postman:
Requisição realizada com método GET para a URL:
`https://viacep.com.br/ws/15991333/json/`

Resultado:

![Print do Teste no Postman](/postman-teste.png)

## Código que fizemos 

<?php
// Verifica se o formulário foi enviado com o campo 'cep'
if (isset($_GET['cep'])) {
    
    // Pega o valor do CEP enviado e remove qualquer caractere que não seja número
    $cep = preg_replace('/[^0-9]/', '', $_GET['cep']);

    // Monta a URL da API do ViaCEP usando o CEP informado
    $url = "https://viacep.com.br/ws/$cep/json/";

    // Faz a requisição para a API e pega a resposta
    $response = file_get_contents($url);

    // Converte a resposta de JSON para um array associativo
    $data = json_decode($response, true);

    // Verifica se a API retornou um erro (CEP inválido)
    if (isset($data['erro'])) {
        echo "CEP não encontrado. Por favor, tente novamente.";
    } else {
        // Se o CEP foi encontrado, mostra as informações na tela
        echo "<h2>Dados do CEP:</h2>";
        echo "Logradouro: " . $data['logradouro'] . "<br>";
        echo "Bairro: " . $data['bairro'] . "<br>";
        echo "Cidade: " . $data['localidade'] . "<br>";
        echo "Estado: " . $data['uf'] . "<br>";
    }
}
?>

<!-- Formulário simples para o usuário digitar o CEP -->
<form method="get">
    <label for="cep">Digite o CEP:</label>
    <input type="text" id="cep" name="cep" required>
    <button type="submit">Buscar</button>
</form>



## Como executar:
- Coloque os arquivos em um servidor local (XAMPP, WAMP, Laragon ou o embutido do PHP).
- Acesse o arquivo `index.php` pelo navegador e consulte CEPs!

