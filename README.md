# NPM

Node Package Manager, ou Gerenciador de Pacotes Node.js, usado para instalar, compartilhar e publicar pacotes de código JavaScript.

# Iniciando o npm

Para iniciar um pacote `npm`, devemos no terminal, digitar:

> npm init

No terminal aparecerá algumas perguntas, como nome do projeto, versão, descrição, ponto de entrada, autor, licença e etc. Nessa parte coloque o que achar necessário. Depois disso aparecerá um arquivo chamado de `package.json`.

Também existe uma outra maneira de criar pacote:

> npm init -y

O `-y` significa **yes for all** (sim para tudo), ou seja, não vai haver nenhuma pergunta.

# Package.json

É um arquivo no formato de JSON (JavaScript Object Notation).

```js
{
  // Abrimos um objeto JS
  // A propriedade sempre será envolvidas com aspas duplas
  // Em seguida, dois pontinhos
  // E finalmente seu valor
  "name": "whatever",
  // Caso tenha um segundo pacote npm, com o mesmo nome pode haver um conflito
  "version": "1.0.0",
  "main": "index.js", 
  // esse aqui é o ponto de entrada, onde estará o código principal
  "scripts": {
    "dev": "node src/file.js"
  // aqui temos os scripts, digamos que é uma outra maneira de escrevermos comandos no terminal
  },
     "author": "Matheus",
     "license": "ISC",
     "keywords": [],
     "description": ""
  }
```

# Instalando dependências

Depois de instalarmos o `cfonts`, utilizando o comando:

> npm install cfonts
> ou...
> npm i cfonts

Vemos que foi iniciado um diretório chamado `node_modules`, e mais um arquivo chamado `package-lock.json`.

E também houve uma adição de código no package.json:

```json
"dependencies": {
  "cfonts": "^3.1.1"
}
```

Foi adicionado um a propriedade para as dependências, então, cada dependências instalada pelo npm, será adicionada aí.

## devDependencies

Ou também podemos instalar como `Dependência de Desenvolvimento`:

> npm i cfonts -D

```json
"devDependencies": {
  "cfonts": "^3.1.1"
}
```

Isso significa que, a dependência será usada apenas em um ambiente de desenvolvimento, ou seja, que são necessárias para o programador desenvolver mas não é necessário a distribuição.

E qualquer alteração no arquivo package.json pode ser atualizado/remapeado para o **package-lock.json** por meio do comando `npm update`.

# node_modules

Ele é um diretório que contém muitas pastas, e o número de pastas vão crescendo de acordo com o números de módulos instalados. O motivo dele ser gigante, é porque cada módulo tem também suas dependências, ou seja, o módulo depende de alguns outros módulos.

Contudo, a pasta **node_modules**, não é enviada ao repositório. Então, na pasta local, é necessário criar um arquivo chamado **.gitignore**, e dentro desse arquivo terá o nome da pasta que o git irá ignorar (node_modules/).

Entretanto, o projeto será distribuído para outras pessoas, mas sem o node_modules, porém, se no projeto estiver o arquivo **package.json**, com todas as dependências necessárias, é possível reinstalar os módulos apartir do comando `npm install`.

# Package-lock

O `package-lock.json` é do formato **.json**, e não é necessário mexer nele enquanto desenvolve, pois ele é responsável por mapear as dependências do seu projeto.

# Criando scripts para rodar no npm via terminal

No package.json, há uma propriedade chamada "scripts", dentro dela podemos colocar os nossos comandos para executar no terminal, sendo muito útil caso o comando seja muito grande.

```json
"scripts": {
  "dev": "node main.js",
},
```

Assim no terminal, escrevemos `npm run dev`, e desse jeito o `node main.js` irá executar.

# Dependências globais

As dependências globais são pacotes que são instalados de forma a serem acessíveis em todo o sistema, ao invés de estarem vinculados apenas a um projeto específico. Isso significa que esses pacotes podem ser usados em qualquer lugar, sem precisar ser instalados novamente.

Instalamos a dependência de forma global, utilizando o `-g` antes do nome da dependência:

```
npm install -g <dependence>
```

E para saber onde se encontra o tal dependência global, usamos o código, `npm root -g`, que vai retornar esse caminho **C:\Users\mathe\AppData\Roaming\npm\node_modules**, e para desinstalar usamos `npm uninstall <dependence> -g`, e para desinstalar um pacote não global é a mesma coisa, apenas tire o `-g`.

# Gerenciando versões das dependências

Depois de instalarmos o módulo `moment`, iremos analisar as versões dele:

```js
{
  "dependencies": {
    "moment": "^2.29.4"
    // major.minor.patch
    // o major "2" é a versão principal do software
    // o minor "29" indica a versão secundária do software
    // o patch "4" significa uma correção de bugs ou pequenas melhorias de desempenho
  }
}
```

Quando você especifica uma dependência com um "^" antes da versão, significa que você está permitindo que o gerenciador de pacotes instale qualquer versão que seja compatível com a versão especificada. Incluindo mudanças significativas ou incompatíveis, o que significa que ela pode afetar a forma como o pacote é usado ou funciona.

Por exemplo, se você especificar uma dependência como "^2.3.1", isso significa que o gerenciador de pacotes pode instalar qualquer versão que comece com "2.3", incluindo "2.3.1", "2.3.2", "2.3.5", etc. No entanto, se uma nova versão "3.0.0" for lançada, o gerenciador de pacotes não a instalará, pois ela é incompatível com a versão especificada "^2.3.1".

Entretanto, temos também o sinal "~" que garante que seu software funcione corretamente com as últimas correções de bugs e melhorias de desempenho, sem se preocupar com a forma como o pacote é usado ou funciona.

O "*" é usado como um curinga que significa qualquer versão.

Se você colocar a versão sem nenhum sinal, a versão não mudará, ficará fixa.

Caso queira mudar para uma versão especifica, utilize o comando `npm i <dependence>@version`, no caso, `npm i moment@1.5.1`, e dependendo da versão pode existir falhas.

Então com o comando `npm outdated`, mostras as versões atuais (current), versão mais desejada (wanted), e a última versão de todos os pacotes que tem nesse projeto (latest). Para atualizar todas os pacotes para a verão mais desejada, utilize o comando `npm upgrade`, você vai notar que o package.json não irá alterar em nada, mais se rodar o comando `npm outdated` de novo, verá que a versão atual do pacotes é a mesma que a versão desejada, pois o mapeamento do package-lock estará atualizado.

Agora para colocar na versão mais atualizada, utilizamos o comando `npm i <dependence>@latest`, no nosso caso `npm i moment@latest`.
