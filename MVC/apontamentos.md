## MVC(Model-View-Controller)

O Model-View-Controller (MVC) é um padrão de arquitetura que separa um aplicativo em três componentes 
lógicos principais: 

- Model: Gerencia dados e lógica de negócios.
- View: lida com layout e exibição.
- Controlador: roteia comandos para as peças do modelo e da visualização.

Cada um desses componentes é construído para lidar com aspectos específicos de desenvolvimento de um aplicativo.
O MVC é uma das estruturas de desenvolvimento web padrão do setor mais usadas para criar projetos escaláveis e extensíveis.

Isso é feito para separar a apresentação dos dados, da lógica de negócio. O desacoplamento desses componentes principais, 
permite uma reutilização eficiente de código e desenvolvimento paralelo.

## Exemplo de controlador de exibição de modelo

Imagine um aplicativo simples de lista de compras. Tudo o que queremos é uma lista do nome, quantidade e preço 
de cada item que precisamos comprar esta semana. 
Abaixo, descreveremos como podemos implementar algumas dessas funcionalidades usando o MVC.

![image](https://user-images.githubusercontent.com/52088444/159123254-4b2430a0-9260-46e7-9f06-df645340574a.png)

**O Model**

O componente Model corresponde a toda a lógica relacionada a dados com a qual o usuário trabalha. 
Isso pode representar os dados que estão sendo transferidos entre os componentes View e Controller 
ou quaisquer outros dados relacionados à lógica de negócios. Por exemplo, um objeto Customer irá 
recuperar as informações do cliente do banco de dados, manipulá-las e atualizá-las de volta para o 
banco de dados ou usá-las para renderizar dados.Ou seja, responsável pela leitura e escrita de dados, 
além de notificar a View quando os dados forem alterados (validações) - ou seja - ele está ligado a manipulação
de dados.

**View**

O componente View é usado para toda a lógica de interface do usuário do aplicativo. Por exemplo, a visualização do 
cliente incluirá todos os componentes da interface do usuário, como caixas de texto, listas suspensas, etc. com os 
quais o usuário final interage.

**Controller**

O controlador contém lógica que atualiza o modelo e/ou visualização em resposta à entrada dos usuários do aplicativo.

Assim, por exemplo, nossa lista de compras pode ter formulários e botões de entrada que nos permitem adicionar ou excluir itens.
Essas ações exigem que o modelo seja atualizado, então a entrada é enviada ao controlador, que então manipula o modelo conforme
apropriado, que envia os dados atualizados para a exibição.

Os controladores atuam como uma interface entre os componentes Model e View para processar toda a lógica de negócios e solicitações 
recebidas, manipular dados usando o componente Model e interagir com as Views para renderizar a saída final. Por exemplo, o 
controlador do Cliente tratará de todas as interações e entradas da Visualização do Cliente e atualizará o banco de dados 
usando o Modelo do Cliente. O mesmo controlador será usado para visualizar os dados do Cliente.


## Como tudo isso realmente funciona?

A imagem abaixo representa o fluxo do MVC em um contexto de Internet, com uma requisição HTTP e resposta em formato HTML.

![image](https://user-images.githubusercontent.com/52088444/159123698-2b6ebcfc-56b6-42f6-9698-567aa07ff615.png)

**Exemplo do funcionamento do MVC**
Você deseja acessar o seu Facebook, mas para isso você precisa logar em uma tela de login, onde precisa digitar seu usuário 
e sua senha. Após a autenticação, caso ocorra tudo certo, o usuário acessa a área restrita do perfil do Facebook, caso contrário
é redirecionado novamente para a página de login repassando uma mensagem que a combinação de usuário e senha é inválida. 
Conseguiu imaginar como o fluxo da imagem?

**O que aconteceu foi algo mais ou menos assim:**

- View – Olá Controller! Um usuário acabou de pedir para acessar o Facebook. Receba os dados de login dele aí.

- Controller – Tranquilo, já te mando a resposta. Espera só alguns segundinhos; – Fala Model, meu parceiro, 
poderia verificar para mim esses dados de login aí e me dizer se ele pode "loga" no sistema.

- Model – Os dados são válidos. Estou te mandando a resposta de login.

- Controller – Obrigado. – View, o usuário informou os dados corretos. Vou mandar para você os dados dele e 
você carrega a página de perfil.

- View – Valeu. Mostrando as informações ao usuário...

## Referencias

- [MVC](https://developer.mozilla.org/en-US/docs/Glossary/MVC)
- [MVC EXEMPLO](https://www.linkedin.com/pulse/o-que-%C3%A9-padr%C3%A3o-de-arquitetura-mvc-alexandre-d%C3%B3rea/?originalSubdomain=pt)



