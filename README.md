Blockchain Deployment and Usage Guide for Take2save
Overview
Este proyecto contiene contratos inteligentes desplegados y verificados en la red de prueba Sepolia. El sistema crea un ecosistema basado en blockchain para el comercio minorista, utilizando tokens para calificaciones, NFTs para productos y certificados representando logros o calificaciones.

Direcciones de los Contratos
Dollar: 0x350a84401eA73c154d0444fd4B3B5FE40E477d64
Product: 0xb30705c5d4b9F20Bc67603e68C28f5b5C58c4166
Speed: 0x36F4369F20A4D7edfAc640288295e1Fcceb4cE9e
Quality: 0x0a37bE346fc079c1e6BF99CC6A9F3b60bA659ec4
Attention: 0xD03fBF207bb3dC2502EA5D572a4106659Db8E96f
Score: 0x1A2AfA89e62405E36F5505D8B8dBe04f5df79854
Certification: 0x480Bc0889f9cdf4f05f3B8b1c3C839677468f31e
Instrucciones de Despliegue
Deployar todos los contratos: Dollar, Product, Speed, Quality, Attention, Score y Certification.

Configurar relaciones entre contratos:

En Dollar, configurar la dirección del contrato Product.
En Product, configurar la dirección del contrato Dollar.
Transferir la propiedad de Speed, Quality y Attention al contrato Score.
En Score, configurar los contratos Speed, Quality y Attention con setContracts.
En Product, configurar la dirección del contrato Score.
En Score, configurar la dirección del contrato Product.
En Certification, configurar los contratos Speed, Quality y Attention.
En Speed, Quality y Attention, configurar la dirección del contrato Certification.
Cargar la metadata de los certificados:
Usar setKind en el contrato Certification para configurar los CIDs de IPFS para cada tipo de certificado (por ejemplo, qualityCID, attentionCID, speedCID).

Instrucciones de Uso
Flujo para Comerciantes
Agregar un nuevo producto: Usar addNewProduct para agregar un producto al sistema.
Ejemplo:
Precio: 10 DOLLAR (10000000000000000000 en wei)
Cantidad: 10 unidades
Dirección del comerciante: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4
Nombre: Torta
Imagen: https://example.com/image.jpg
Descripción: La mejor torta de todas
Estado: false (no usado)
Flujo para Usuarios
Compra (Mintear NFTs de productos):
Llamar a safeMint con el ID del producto y la cantidad deseada. Por ejemplo, para comprar 1 unidad del producto con ID 0.

Calificación (Enviar puntuaciones):
Llamar a score para enviar calificaciones de velocidad, calidad y atención. Asegurarse de poseer el NFT del producto y de no haberlo calificado antes.

Certificación (Mintear certificados):
Llamar a safeMint en el contrato Certification, especificando el tipo de certificado (por ejemplo, qualityCID). Asegurarse de tener suficientes tokens (10 de Speed, Quality o Attention).

Información sobre ABIs
Puedes obtener las ABIs de cada contrato desde Etherscan Sepolia utilizando las direcciones de los contratos listadas anteriormente.

Funciones Clave
Agregar un nuevo producto:
addNewProduct(Sproduct calldata _product)
La estructura Sproduct contiene: precio, cantidad, dirección del comerciante, nombre, imagen, descripción y estado (bool usado).

Mintear NFTs de productos:
safeMint(uint256 _idOfProduct, uint256 _quantity)
Donde _idOfProduct es el ID del producto y _quantity es la cantidad deseada.

Enviar calificaciones:
score(uint _qual, uint _spd, uint _atte, uint tokenId)
Donde _qual, _spd y _atte son las calificaciones y tokenId es el ID del NFT del producto.

Mintear certificados:
safeMint(string memory _scoreKind)
Donde _scoreKind es uno de los valores: qualityCID, attentionCID o speedCID.

Recursos Adicionales
Para una explicación detallada del flujo de usuario y la interacción con los contratos inteligentes, consulta este video explicativo:
https://youtu.be/r6n1Dfh2H-Q