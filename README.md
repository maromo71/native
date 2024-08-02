# Introdução ao React Native
## Material disponibilizado no Teams

### Ferramenta Expo

O Expo é uma plataforma abrangente para o desenvolvimento de aplicativos móveis usando React Native. Ela simplifica o processo de criação, desenvolvimento e distribuição de aplicativos, fornecendo um conjunto de ferramentas e serviços que eliminam a necessidade de configurações complexas de build nativas. Com o Expo, desenvolvedores podem começar rapidamente a construir aplicativos móveis usando apenas JavaScript e o framework React Native, beneficiando-se de um ambiente de desenvolvimento integrado que inclui uma aplicação cliente para testar instantaneamente as alterações no código em dispositivos móveis reais ou emuladores. Além disso, o Expo oferece acesso a APIs nativas, atualizações over-the-air e um ecossistema de plugins que facilitam a integração de funcionalidades adicionais, tornando o desenvolvimento de aplicativos mais acessível e eficiente para desenvolvedores de todos os níveis de habilidade.

<p align="center">
  <a href="https://expo.dev/">
    <img alt="banner expo" height="128" src="./resources/banner.png">
    <h1 align="center">Expo</h1>
  </a>
</p>

### Instalação do Expo

Para instalar o Expo e começar a desenvolver aplicativos com React Native, siga este passo a passo:

**1. Instalar Node.js e npm**
O Expo requer o Node.js e o npm (Node Package Manager) para funcionar. Baixe e instale a versão mais recente do Node.js a partir do site oficial: Node.js. O npm é instalado automaticamente junto com o Node.js.

**2. Instalar Expo CLI**
Expo CLI é a ferramenta de linha de comando que você usará para criar e gerenciar seus projetos Expo.

Abra o terminal (ou prompt de comando no Windows) e execute o seguinte comando para instalar o Expo CLI globalmente:

```bash
npm install --global expo-cli
```

Este comando pode exigir permissões de administrador. Se você estiver no Linux ou macOS, pode ser necessário adicionar sudo antes do comando.

**3. Criar um Novo Projeto Expo**
Depois de instalar o Expo CLI, você pode criar um novo projeto com o seguinte comando:

```bash
expo init my-new-project
```

Substitua my-new-project pelo nome do seu projeto. 
O CLI perguntará qual tipo de projeto você deseja criar. 
Você pode escolher entre opções como um projeto **em branco (blank)** [nosso caso], com TypeScript, ou um exemplo pré-configurado.

**4. Executar o Projeto**
Para iniciar o servidor de desenvolvimento, navegue até o diretório do projeto recém-criado e execute:

```bash
cd my-new-project
expo start
```

Este comando abrirá a ferramenta Expo Developer Tools em seu navegador e fornecerá um QR code que você pode escanear com o aplicativo Expo Go em um dispositivo móvel.

**5. Instalar Expo Go**
Para visualizar seu aplicativo em um dispositivo físico, instale o aplicativo Expo Go a partir da Google Play Store ou da Apple App Store. Em seguida, use o aplicativo para escanear o QR code fornecido pelo Expo Developer Tools.

**6. Desenvolvimento Contínuo**
Enquanto o Expo CLI estiver rodando, quaisquer mudanças feitas no código do seu projeto serão atualizadas automaticamente no dispositivo ou emulador que você está usando para testar.

Para mais detalhes e configurações avançadas, você pode consultar a documentação oficial do Expo.

Este guia cobre o básico para começar com o Expo, mas a documentação oficial e a comunidade Expo são excelentes recursos para aprofundar-se mais nas funcionalidades e capacidades avançadas do Expo​.

**7 Para execução em um Browser, caso não consiga pelo Mobile**

**7.1 Passos para Executar um Projeto Expo no Ambiente Web**

***Instalar Dependências para o Ambiente Web:***
Primeiro, você precisa instalar as bibliotecas necessárias para executar seu projeto Expo no navegador. Execute o seguinte comando no diretório do seu projeto:

```bash
npx expo install react-native-web react-dom @expo/metro-runtime
```

Estas bibliotecas permitem que você use componentes React Native na web.
Configurar o Projeto para Web:
Certifique-se de que o seu projeto Expo está configurado para a web. Se você criou o projeto usando versões recentes do Expo, ele já deve estar configurado, mas você pode verificar as configurações no arquivo app.json.

```json
{
  "expo": {
    "platforms": ["ios", "android", "web"]
  }
}
```

Isso garante que a plataforma web esteja incluída nas configurações do projeto.
Iniciar o Servidor Expo para Web:
Agora, você pode iniciar o projeto usando o Expo CLI com suporte para web:

```bash
npx expo start --web
```

Este comando iniciará o Expo Developer Tools, e seu aplicativo será acessível através de um navegador web.

***Testar o Aplicativo no Navegador:***
Após iniciar o servidor, o Expo Developer Tools fornecerá um URL local (normalmente http://localhost:19006) onde você pode visualizar seu aplicativo no navegador. Abra este URL no Chrome ou em qualquer outro navegador compatível.
Solução de Problemas e Logs:
Problemas com Dependências: Se encontrar erros relacionados a pacotes ou dependências, tente limpar o cache do npm e reinstalar as dependências:

```bash
npm cache clean --force

npm install
```

Verificar Logs: Use os logs no terminal e no console do navegador para depurar qualquer problema que ocorra ao executar o aplicativo.
***Recursos Adicionais***
**Documentação do Expo para Web** - Guia completo sobre como usar o Expo para desenvolvimento web.
**React Native para Web** - Documentação oficial sobre como usar componentes React Native na web.
Seguindo esses passos, você deve conseguir executar seu projeto Expo no ambiente web com sucesso. Se houver problemas específicos durante o processo, consulte a documentação ou procure mais ajuda nos fóruns da comunidade Expo.
