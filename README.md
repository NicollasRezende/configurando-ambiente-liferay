# Guia de Configuração do Ambiente para Liferay DXP

## Requisitos

- **Java**: Versão **8**
- **Node.js**: Versão **16**

### Gerenciamento de Versões

Para facilitar a troca de versões entre diferentes projetos, recomenda-se:

- **Node.js**: Utilize o `nvm` (Node Version Manager)
- **Java**: Utilize o `jdk` apropriado para gerenciar as versões no seu ambiente

Certifique-se de que ambas as versões estejam instaladas corretamente.

---

## Inicialização do Workspace

Para iniciar um workspace do Liferay DXP, execute os seguintes comandos:

```sh
blade init nome-projeto -v portal-7.4-ga112
cd nome-projeto
blade server init
```

O workspace será inicializado com sucesso!

### Alternativa

#### Executando o Liferay DXP localmente

```sh
my-project $ blade gw initBundle
my-project $ blade gw deploy
my-project $ blade server run
```

#### Executando o Liferay DXP em um contêiner Docker

```sh
my-project $ blade gw createDockerContainer
my-project $ blade gw startDockerContainer
```

---

## Geração de Tema no Liferay

### Dependências Necessárias

Certifique-se de que possui as ferramentas **Gulp** e **Yeoman** instaladas globalmente:

```sh
npm install -g gulp
npm install -g generator-liferay-theme
```

Alternativamente, pode-se utilizar o comando:

```sh
yo liferay-theme
```

Siga as etapas de instalação conforme solicitado.

### Configuração do Tema

1. Acesse a pasta `tomcat` do seu workspace.
2. Copie o caminho completo e insira no comando:

   ```sh
   gulp init
   ```
3. Dentro da pasta raiz do tema, instale todas as dependências:

   ```sh
   npm install
   ```

4. Edite o arquivo `package.json` para ajustar as configurações do tema:

   - Desative o **Dart Sass**, adicionando o seguinte trecho:

   ```json
   "liferayTheme": {
       "baseTheme": "styled",
       "fontAwesome": false,
       "templateLanguage": "ftl",
       "version": "7.4",
       "sassOptions": {
           "dartSass": "false"
       }
   }
   ```

   - Adicione a dependência do `gulp-sass` dentro de **devDependencies**:

   ```json
   "devDependencies": {
       "compass-mixins": "0.12.10",
       "gulp": "4.0.2",
       "gulp-sass": "5.1.0",
       "liferay-frontend-css-common": "6.0.8",
       "liferay-frontend-theme-styled": "6.0.54",
       "liferay-frontend-theme-unstyled": "6.0.45",
       "liferay-theme-tasks": "^11.5.5"
   }
   ```

   - Adicione a seguinte dependência no final do arquivo, dentro de **dependencies**:

   ```json
   "dependencies": {
       "node-sass": "8.0.0"
   }
   ```

### Finalização da Configuração

1. Apague as pastas `build` e `node_modules`:

   ```sh
   rm -rf build node_modules
   ```

2. Instale novamente as dependências:

   ```sh
   npm install
   ```

3. Compile o tema:

   ```sh
   gulp build
   ```

Tema iniciado com sucesso! 🎉

