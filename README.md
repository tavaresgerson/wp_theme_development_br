# Desenvolvimento de Temas no WordPress

Este artigo é sobre o desenvolvimento de temas do WordPress. Se você deseja saber mais sobre como instalar e usar Temas, consulte Usando Temas. Este tópico difere de [Usando Temas](https://codex.wordpress.org/Using_Themes) porque discute os aspectos técnicos de escrever código para construir seus próprios Temas.

## Porquê temas WordPress

Temas WordPress são arquivos que trabalham juntos para criar o design e a funcionalidade de um site WordPress. Cada tema pode ser diferente, oferecendo muitas opções para os proprietários de sites alterarem instantaneamente a aparência do seu site.

Você pode desenvolver temas para seu uso particular, para o projeto de um cliente ou enviar para o repositório de temas [oficiais do WordPress](https://codex.wordpress.org/Theme_Review). Gostaria de mais motivos para construir um tema no WordPress?

* Para criar uma aparência única no seu site WordPress
* Para aproveitar os [modelos], [tags] de modelo e o [Loop do WordPress] para gerar diferentes resultados e aparências do site.
* Para fornecer templates alternativos para recursos específicos do site, como páginas de [categorias] e páginas de resultados de pesquisa.
* Para alternar rapidamente entre dois layouts de site ou aproveitar um [alternador de tema] ou estilo para permitir que os proprietários do site modifiquem a aparência

Um tema WordPress também tem muitos benefícios.

* Ele separa os estilos de apresentação e os arquivos de templates do sistema para que o site seja atualizado sem alterações drásticas na apresentação visual do site.
* Permite a personalização de funções do site de forma exclusiva para o tema
* Permite mudanças rápidas no design visual e layout de um site WordPress
* Elimina a necessidade de um proprietário do WordPress típico aprender CSS, HTML e PHP para ter um site de ótima aparência

Porquê você deve construir seu próprio tema WordPress? Essa é a pergunta verdadeira

* É uma oportunidade para aprender mais sobre CSS, HTML e PHP
* Oportunidade de colocar sua experiência com CSS, HTML e PHP para trabalhar
* Criatividade
* Diversão (na maioria das vezes)
* Se definir como tema público, você pode se sentir bem por ter compartilhado e devolvido algo à Comunidade WordPress (ok, direito de se gabar)

## Padrões de Desenvolvimento de Temas

Os temas do WordPress devem ser codificados usando os seguintes padrões:

* Use PHP bem estruturado e sem erros e com HTML válido. Consulte [Padrões de codificação do WordPress]
* Use CSS limpo e válido. Consulte [Padrões de codificação CSS].
* Siga as diretrizes de design em [Design e layout do site].

## Anatomia de um tema
Os temas do WordPress ficam em subdiretórios do diretório de temas do WordPress (`wp-content/themes/` por padrão) que [não podem ser movidos diretamente] usando o arquivo `wp-config.php`. O subdiretório do Tema contém todos os arquivos de folha de estilo do Tema, arquivos de template, arquivo de funções opcionais (`functions.php`) e arquivos Javascript e imagens. Por exemplo, um tema chamado "teste" estaria disponível no diretório `wp-content/themes/test/`. Evite usar números para o nome do tema, pois isso impede que ele seja exibido na lista de temas disponíveis.

O WordPress inclui um tema padrão em cada nova instalação. Examine os arquivos no tema padrão com cuidado para ter uma ideia melhor de como criar seus próprios arquivos de tema.

Para um guia visual, veja este [infográfico sobre WordPress Theme Anatomy](https://yoast.com/wordpress-theme-anatomy/)

Os temas do WordPress normalmente consistem em três tipos principais de arquivos, além de imagens e arquivos Javascript.

1. A folha de estilo chamada style.css, que controla a apresentação (design visual e layout) das páginas do site
2. [Arquivos de template do WordPress] que controlam a maneira como as páginas do site geram as informações do banco de dados para serem exibidas no site
3. O arquivo de funções opcionais (`functions.php`) como parte dos arquivos do WordPress Theme

Vamos olhar para eles individualmente

### Temas filhos

O tema mais simples possível é um tema filho que inclui apenas um arquivo style.css, além de quaisquer imagens. Isso é possível porquê é filho de outro tema que atua como pai.

Para obter um guia detalhado sobre temas filhos, consulte [Temas filhos].

## Folha de estilo do tema

Além das informações de estilo CSS para seu tema, `style.css` fornece detalhes sobre o tema na forma de comentários. Dois temas não podem ter os mesmos detalhes listados em seus [cabeçalhos] de comentários, pois isso causará problemas na caixa de diálogo de seleção de temas. Se você criar seu próprio tema copiando um já existente, certifique-se de alterar essas informações primeiro.

O seguinte é um exemplo das primeiras linhas da folha de estilo, chamada de cabeçalho da folha de estilo, para o tema "Twenty Thirteen"

```css
/*
Theme Name: Twenty Thirteen
Theme URI: http://wordpress.org/themes/twentythirteen
Author: the WordPress team
Author URI: http://wordpress.org/
Description: The 2013 theme for WordPress takes us back to the blog, featuring a full range of post formats, each displayed beautifully in their own unique way. Design details abound, starting with a vibrant color scheme and matching header images, beautiful typography and icons, and a flexible layout that looks great on any device, big or small.
Version: 1.0
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Tags: black, brown, orange, tan, white, yellow, light, one-column, two-columns, right-sidebar, flexible-width, custom-header, custom-menu, editor-style, featured-images, microformats, post-formats, rtl-language-support, sticky-post, translation-ready
Text Domain: twentythirteen

This theme, like WordPress, is licensed under the GPL.
Use it to make something cool, have fun, and share what you've learned with others.
*/
```

> NB: Sugere-se que o nome usado para o autor seja o mesmo nome de usuário wordpress.org do autor do tema, embora também possa ser o nome real do autor. A estolha é do Autor do Tema.

Observe a lista de Tags usada para descrever o tema. Eles permitem que o usuário encontre seu tema usando o filtro de tags. Você pode encontrar uma lista completa do [Theme Review Handbook].

As linhas de cabeçalho de comentário em style.css são necessárias para que o WordPress possa identificar o Tema e exibi-lo no Painel de Administração em Design > Temas como opção de tema disponível junto com qualquer outro tema instalado.

### Diretrizes da folha de estilo
* Siga os [padrões de codificação CSS] ao criar seu CSS
* Use CSS válido quando possível. Como exceção, use prefixos específicos do fornecedor para aproveitar os recursos do CSS3
* Minimize os hacks de CSS. A exceção óbvia é o suporte específico para navegadores, geralmente versões do IE. Se possível, separe os hacks de CSS em seções ou arquivos separados.
* Todos os elementos HTML possíveis deve ser estilizados pelo seu tema (a menos que seja um tema filho), tanto no conteúdo do post/página quanto no conteúdo do comentário.
* Tabelas, legendas, imagens, listas, citações em bloco, etc
* A adição de estilos amigáveis para impressão é altamente recomendada.
  * Você pode incluir uma folha de impressão com `media="print"` ou adicionar um bloco de mídia de impressão em sua folha de estilo principal

## Arquivo de funções
Um tema pode opcionalmente usar um arquivo de funções que reside no subdiretório do tema e é chamado de `functions.php`. Esse arquivo basicamente funciona como um plugin, e se estiver presente no tema que você está usando, ele é carregado automaticamente durante a inicialização do WordPress (tanto para páginas de administração quanto para páginas externas). Usos sugeridos para este arquivo:

* Enfileirar folhas de estilo e scripts do tema. Consulte [wp_enqueue_scripts](https://codex.wordpress.org/Plugin_API/Action_Reference/wp_enqueue_scripts)
* Ative [recursos de tema](https://codex.wordpress.org/Theme_Features), como [barras laterais](https://codex.wordpress.org/Sidebars), [menus de navegação](https://codex.wordpress.org/Navigation_Menus), [miniaturas de postagem](https://codex.wordpress.org/Post_Thumbnails), [formatos de postagem](https://codex.wordpress.org/Post_Formats), [cabeçalhos personalizados](https://codex.wordpress.org/Custom_Headers), [planos de fundo personalizados](https://codex.wordpress.org/Custom_Backgrounds) e outros.
* Defina funções usadas em vários arquivos de template do seu tema
* Configure um menu de opções, dando aos proprietários do site opções de cores, estilos e outros aspectos do seu tema.

O tema padrão do WordPress contém um arquivo `functions.php` que define muitos desses recursos, então você pode querer usá-lo como modelo. Como o `functions.php` funciona basicamente como um plugin, a lista [Function_Reference](https://codex.wordpress.org/Function_Reference) é o melhor lugar para obter mais informações sobre o que você pode fazer com este arquivo.

**Nota para decidir quando adicionar funções a `functions.php` ou a um plugin específico:** você pode achar necessário que a mesma função esteja disponível para mais de um tema pai. Se for esse o caso, a função deve ser criada em um [plugin](https://codex.wordpress.org/Plugins) ao invés de um `functions.php` para o tema específico. Isso pode incluir tags de template e outras funções específicas. As funções contidas nos plugins serão vistas por todos os temas.

### Arquivos de template
[Os templates](https://codex.wordpress.org/Stepping_Into_Templates) são arquivos de origem PHP usados para gerar as páginas solicitadas pelos visitantes e são gerados como HTML. Os arquivos de modelo são compostos de HTML, PHP e Tags de template do WordPress.

Vejamos os vários modelos que podem ser definidos como parte de um tema.

O WordPress permite que você defina templates separados para os vários aspectos do seu site. No entanto, não é essencial ter todos esses arquivos de modelo diferentes para que seu site funcione totalmente. Os templates são escolhidos e gerados com base na hierarquia de modelos, dependendo de quais templates estão disponíveis em um tema específico.

Como desenvolvedor de temas, você pode escolher a quantidade de personalização que deseja implementar usando modelos. Por exemplo, como um caso extremo, você pode usar apenas um arquivo de modelo, chamado `index.php` como modelo para todas as páginas geradas e exibidas pelo site. Um uso mais comum é fazer com que diferentes arquivos de template gerem resultados diferentes, para permitir a máxima personalização.

#### Lista de arquivos de template

Aqui está a lista dos arquivos de tema reconhecidos pelo WordPress. Claro, seu tema pode conter quaisquer outras folhas de estilo, imagens ou arquivos. Apenas lembre-se de que o conteúdo seguinte tem um significado especial para o WordPress - consulte à [hierarquia de templates](https://codex.wordpress.org/Template_Hierarchy) para obter mais informações

`style.css` A folha de estilo principal. Isso **deve** ser incluído no seu tema e deve conter o cabeçalho de informações.

`rtl.css` Isso será incluído automaticamente se a direção do texto do seu site for da direita para a esquerda. Isso pode ser gerado usando o [plugin RTLer](http://wordpress.org/extend/plugins/rtler/).

`index.php` O template principal. Se seu tema fornece seus próprios templates, `index.php deve estar presente.

`comments.php` O template de comentários

`front-page.php` O template da primeira página

`home.php` O template de página inicial, que é a primeira página por padrão. Se você usa uma página inicial estática este é o modelo para a página com as postagens mais recents.

`single.php` O template de postagem única. Usado quando uma única postagem é consultada. Para este e todos os outros templates de consulta, `index.php` é usado se o modelo de consulta não estiver presente.

`single-{post-type}.php` O template de postagem única usada quando uma única postagem de um tipos personalizado é consultada. Por exemplo, `single-book.php` seria usado para exibir postagens únicos do tipo de postagem personalizado chamado "livro". `index.php` é usado se o modelo de consulta para o tipo de postagem personalizado não estiver presente.

`page.php` O template para página. Usado quando uma [página individual](https://codex.wordpress.org/Pages) é consultada

`category.php` O [template de categoria](https://codex.wordpress.org/Category_Templates). Usado quando uma categoria é consultada.

`tag.php` O [template de tags](https://codex.wordpress.org/Tag_Templates). Usado quando uma tag é consultada

`taxonomy.php` o template de taxonomia, usado quando um termo em uma taxonomia personalizada é consultada.

`author.php` o [template de autor](https://codex.wordpress.org/Author_Templates). Usado quando um autor é consultado

`date.php` O template de data/hora. Usado quando uma data ou hora é consultada. Ano, mês, dia, hora, minuto, segundo

`archive.php` O modelo de arquivo. Usado quando uma categoria, autor ou data é consultada. Observe que este modelo será substituído por `category.php` e `date.php` para seus respectivos tipos de consulta.

`search.php` O template de resultados da pesquisa, usado quando uma pesquisa é realizada.

`attachment.php` O template de anexo, usado para visualizar um único anexo

`image.php` O template de anexo de imagem. Usado ao visualizar um único anexo de imagem. Se não estiver presente, attachment.php será usado.

`404.php` O [template 404](https://codex.wordpress.org/Creating_an_Error_404_Page) não encontrado. Usado quando o WordPress não consegue encontrar um post ou página que corresponda à consulta.

Esses arquivos tem um significado especial em relação ao WordPress, pois são usados em substituição ao `index.php`, quando disponível, de acordo com a [Hierarquia de Templates](https://codex.wordpress.org/Template_Hierarchy), e quando a [Tag Condicional](https://codex.wordpress.org/Conditional_Tags) correspondente retornar `true`. Por exemplo, se apenas um único post estiver sendo exibido, a função `is_single()` retornará `true` e, se houver um arquivo `single.php` no tema ativo, esse modelo será usado para gerar a página.

#### Templates básicos

No mínimo, um tema WordPress consiste em dois arquivos:

* style.css
* index.php

Ambos os arquivos vão para o diretório Theme. O [arquivo de template](https://codex.wordpress.org/Stepping_Into_Templates) `index.php` é muito fléxivel. Ele pode ser usado para incluir todas as referências ao cabeçalho, barra lateral, rodapé, conteúdo, categorias, arquivos, pesquisa, erro e qualquer outra página criada no WordPress.

Ou pode ser dividido em arquivos de templates modulares, cada um assumindo parte da carga de trabalho. Se você não fornecer outros arquivos de template, o WordPress pode ter arquivos ou funções padrão para realizar seus trabalhos. Por exemplo, se você não fornecer um arquivo de modelo `searchform.php`, o WordPress terá uma função padrão para exibir o formulário de pesquisa.

Os arquivos de template típicos incluem:

* `comments.php`
* `comments-popup.php`
* `footer.php`
* `header.php`
* `sidebar.php`

Usando esses arquivos de template, você pode colocar tags de temmplate no arquivo mestre `index.php` para incluir esses outros arquivos onde você deseja que eles apareçam na página final gerada.

* Para incluir o cabeçalho, use `get_header()`
* Para incluir a barra lateral, use `get_sidebar()`
* Para incluir o rodapé, use `get_footer()`
* Para incluir o formulário de pesquisa, use `get_search_form()`

Aqui está um exemplo do uso de `include`:

```php
<?php get_sidebar() ?>
<?php get_footer() ?>
```

Os arquivos padrão para algumas funções de template podem estar obsoletos ou não estão presentes, e você deve fornecer esses arquivos em seu tema. A partir da versão 3.0, os arquivos padrão obsoletos estão localizados em `wp-includes/theme-compat`. Por exemplo, você deve fornecer `header.php` para que a função `get_header()` funcione com segurança e `comments.php` para a função `comments_template()`.

Para saber mais sobre como esses vários templates funcionam e como gerar informações diferentes dentro deles, leia a documentação dos [templates](https://codex.wordpress.org/Templates).

#### Templates de páginas personalizados

Os arquivos que definem cada template de página são encontrados em seu diretório de [temas](https://codex.wordpress.org/Using_Themes). Para criar um novo template de página personalizado para uma página, você deve criar um arquivo. Vamos chamar nosso template de primeira página para nossa página `snarfer.php`. No topo do arquivo `snarfer.php`, coloque o seguinte:

```php
<?php
/*
Template Name: Snarfer
*/
?>
```

O código acima define este arquivo `snarfer.php` como o template "Snarfer". Naturalmente, "Snarfer" pode ser substituído por qualquer texto para alterar o nome do template de página. Este nome de template aparecerá no Editor de Temas como também o link para editar este arquivo.

O arquivo pode ser nomeado quase com qualquer coisas mas, com a extensão `.php` (veja nomes de arquivos de temas reservados. Estes nomes são usados para propósitos específicos no WordPress).

O que segue as cinco linhas de código acima é com você. O restante do código que você escrever controlará como as páginas que usam o template de página Snarfer serão exibidas. Consulte [Tags de template] para obter uma descrição das várias funções de template do WordPress que você pode usar para essa finalidade. Você pode achar mais conveniente copiar algum outro modelo (talvez, `page.php` ou `index.php`) para `snarfer.php` e então adicionar as cinco linhas de código acima no início do arquivo. Dessa forma, você só terá que alterar o código HTML e PHP em vez de criar tudo do zero. Exemplos são mostrados abaixo. Depois de criar um template de página e colocá-lo no diretório do seu tema, ele estará disponível como opção ao criar ou editar uma página (Nota: ao criar ou editar uma página, a oção Template de página não aparece a menos que haja pelo menos um template definido da maneira citada anteriormente).

#### Arquivos de template baseados em consulta

O WordPress pode carregar diferentes [templates](https://codex.wordpress.org/Stepping_Into_Templates) para diferentes tipos de consulta. Há duas maneiras de fazer isso: como parte da [hierarquia de templates](https://codex.wordpress.org/Template_Hierarchy) integrada e por meio do uso de [tags condicionais](https://codex.wordpress.org/Conditional_Tags) dentro do [loop](https://codex.wordpress.org/The_Loop) de um arquivo de template.

Para usar a Hierarquia de Templates, você basicamente precisa fornecer arquivos Template com propósitos especiais, que serão usados automaticamente para substituir o `index.php`. Por exemplo, se o seu tema fornece um modelo chamado `category.php`e uma categoria está sendo consultada, `category.php` será carregado em vez de `index.php`. Se `category.php` não estiver presente, `index.php` é usado normalmente.

Você pode ser ainda mais específico na hierarquia de modelos fornecendo um arquivo chamado, por exemplo, `category-6.php` -- este arquivo será usado em vez de `category.php` ao gerar a página para a categoria cujo número de ID é 6. (Você pod encontar números de ID de categoria em [Gerenciar](https://codex.wordpress.org/Administration_Panels#Manage_-_Change_your_content) > [Categorias](https://codex.wordpress.org/Administration_Panels#Categories) se estiver conectado como administrador do site no WordPress versão 2.3 e inferior. No WordPress 2.5, a coluna ID foi removida dos painéis de administração. Você pode localizar o ID da categoria clicando em "Editar categoria" e procurando na barra de ednereços do URL pelo valor cat_ID. Ele irá ver '...categories.php?action=edit&cat_ID=3' onde '3' é o id da categoria). Para uma visão mais detalhada de como esse processo funciona, consulte [Templates de Categoria](https://codex.wordpress.org/Category_Templates).

Se o seu tema precisa ter ainda mais controle sobre quais arquivos de template são usados do que o fornecido na [Hierarquia de templates](https://codex.wordpress.org/Template_Hierarchy), você pod usar [tags condicionais](https://codex.wordpress.org/Conditional_Tags). A Tag Condicional basicamente verifica se alguma condição específica é verdadeira, dentro do [Loop do WordPress](https://codex.wordpress.org/The_Loop_in_Action) e então você pode carregar um template específico ou colocar algum texto específico na tela com base nessa condição.

Por exemplo, para gerar uma folha de estilo distinta em uma postagem eonctrada apenas em uma categoria específica, o código pode ficar assim:

```php
<?php
if ( is_category( '9' ) ) {
    get_template_part('single2'); // procurando posts na categoria com ID '9'
} senão {
    get_template_part('single1'); // coloque isso em todos os outros posts de categoria
}
?>
```

Ou usando uma consulta, pode ser assim:
```php
<?php
$post = $wp_query->post;
if ( in_category( '9' ) ) {
    get_template_part('single2');
} senão {
    get_template_part('single1');
}
?>
```

Em ambos os casos, este código de exemplo fará com que diferentes templates sejam usados dependendo da categoria da postagem específica que está sendo exibida. As condições de consulta não estão limitadas a categorias, no entanto, consulte o artigo [Tags condicionais](https://codex.wordpress.org/Conditional_Tags) para ver todas as opções.

#### Definindo templates personalizados
É possível usar o sistema de plugins do WordPress para definir modelos adicionais que são mostrados com base em seus próprios critérios personalizados. [Esse recurso avançado pode ser realizado usando o gancho de ação](https://codex.wordpress.org/Plugin_API#Current_Hooks_For_Actions) 'template_include'. Mais informações sobre criação de plug-ins podem ser encontradas na referência da [API do plug-in](https://codex.wordpress.org/Plugin_API).

#### Incluindo arquivos de template

Para carregar outro template (além de header, sidebar, footer, que tem comandos incluídos predefinidos como `get_header()` em um template, você pode usar `get_template_part()`. Isso torna mais fácil para um tema reutilizar seções de código.

Exemplo: suponha que você tenha um template no diretório 'template-parts' chamado `blog-content.php` no diretório raiz do seu tema. Para chamar este modelo, use este código.

```php
<?php get_template_part('template-parts/blog', 'conteúdo'); ?>
```

Exemplo 2: Suponha que você tenha vários tipos de postagem, como postagem, livro, página. você pode criar modelos no diretório raiz do seu tema como `content-post.php`, `content-book.php`, `content-page.php` Agora, chame esses modelos facilmente sob o loop como:

```php 
<?php get_template_part('content', get_post_type()); ?>
```

#### Referenciando arquivos de um template

Ao fazer referência a outros arquivos dentro do mesmo tema, evite URIs codificados e caminhos de arquivo. Em vez disso, faça referência aos URIs e caminhos de arquivo com `bloginfo()`: consulte Referenciando arquivos de um template nesta seção.

Observe que os URIs usados na folha de estilo são relativos à folha de estilo, não à página que faz referência à folha de estilo. Por exemplo, se você incluir um diretório `images/` em seu tema, você só precisa específicar esse diretório relativo no CSS, assim:

```css
h1 {
    imagem de fundo: url(imagens/meu-fundo.jpg);
}
```

#### Ganchos de API do plug-in

Ao desenvolver temas, é bom ter em mente que seu tema deve ser configurado para que possa funcionar bem com qualquer plugin do WordPress que os usuários decidam instalar. Os plug-ins adicionam funcionalidade ao WordPress por meio de "Ganchos de ação" (consulte [API do plug-in](https://codex.wordpress.org/Plugin_API) para obter mais informações).

A maioria dos Ganchos de Ação (Action Hooks) está dentro do código PHP principal do WordPress, então seu tema não precisa ter nenhuma tag especial para funcionar. Mas, alguns ganchos de ação precisam estar presentes em seu tema, para que os plug-ins exibam informações diretamente em seu cabeçalho, rodapé, barra lateral ou no corpo da página. Aqui está uma lista das tags de ganchos para templates com ações especiais que você precisa incluir:

- [`wp_enqueue_scripts`](https://codex.wordpress.org/Plugin_API/Action_Reference/wp_enqueue_scripts): Usado no arquivo de funções do tema. Usado para carregar scripts externos e folhas de estilo.
- [`wp_head()`](https://codex.wordpress.org/Function_Reference/wp_head): Usado dentro da tag `<head></head>` de um tema, em `header.php`. Exemplo de uso do plugin: adicionar código Javascript.
- [`wp_footer()`](https://codex.wordpress.org/Function_Reference/wp_footer): Usado no `footer.php`, logo antes da tag de fechamento `<body>`. Exemplo de uso de plugin: insira um código PHP que precisa ser executado após todo o resto, na parte inferior do rodapé. Muito comumente usado para inserir código de estatísticas da web como o Google Analytics, por exemplo.
- [`wp_meta()`](https://codex.wordpress.org/Function_Reference/wp_meta): Normalmente vai na seção `<li>Meta</li>` do menu ou barra lateral de um tema: `sidebar.php`. Exemplo de uso de plugin: inclua um anúncio rotativo ou uma nuvem de tags.
- [`comment_form()`](https://codex.wordpress.org/Function_Reference/comment_form): Usado em `comments.php` diretamente antes da tag de fechamento do arquivo `</div>`. Exxemplo de uso de plugin: exibir uma visualização de comentário.

Para um exemplo de uso no mundo real, você encontrará esses ganchos de plugin incluídos nos modelos padrão do tema.

#### API de personalização de temas

A partir do WordPress 3.4, um novo recurso de personalização de temas está disponível por padrão para quase todos os temas do WordPress. A página de administração de personalização do tema é preenchida automaticamente com opções para as quais um tema declara suporte com `add_theme_support()` ou usando a API de configurações e permite que os administradores vejam visualizações não permanentes das alterações feitas em tempo-real.

Desenvolvedores de temas e plugins interessados em adicionar novas opções à página de personalização de temas de um tema devem consultar a documentação na [API de personalização]() de temas. Tutoriais adicionais sobre a API de personalização de temas estão disponíveis no site [Ottopress.com](http://ottopress.com/2012/how-to-leverage-the-theme-customizer-in-your-own-themes/).

#### Dados não confiáveis

Você deve escapar do conteúdo gerado dinamicamente em seu tema, especialmente o conteúdo que é enviado para atributos HTML. COnforme observado em [Padrões de codificação do WordPress](http://make.wordpress.org/core/handbook/coding-standards/), o texto que entra nos atributos deve ser executado por meio de [`esc_attr()`](https://codex.wordpress.org/Function_Reference/esc_attr) para que aspas simples ou duplas não terminem o valor do atributo e invalidem o XHTML e causem um problema de segurança. Lugares comuns para verificar são os atributos `title`, `alt` e `value`.

Existem algumas tags de modo especiais para casos comuns em que a saída segura é necessária. Um desses casos envolve a saída de um título de postagem para um atributo `title` usando [`the_title_attribute()`](https://codex.wordpress.org/Function_Reference/the_title_attribute) em vez de [`the_title()`](https://codex.wordpress.org/Function_Reference/the_title) para evitar uma vulnerabilidade de segurança. Aqui está um exemplo de escape correto para o atributo `title` de um link de postagem ao usar texto traduzível.

```php
<a href="<?php the_permalink(); ?>" title="<?php sprintf( __( 'Link permanente para %s', 'theme-name' ), the_title_attribute( 'echo=0' ) ); ?>"><?php the_title(); ?></a>
```

Substitua as chamadas de escape obsoletas pelas chamadas corretas: [`wp_specialchars()`](https://codex.wordpress.org/Function_Reference/wp_specialchars) e [`htmlspecialchars`](http://php.net/manual/en/function.htmlspecialchars.php) por [`esc_html`](https://codex.wordpress.org/Function_Reference/esc_html), [`clean_url`](https://codex.wordpress.org/Function_Reference/clean_url) por [`esc_url`](https://codex.wordpress.org/Function_Reference/esc_url) e [`attribute_escape`](https://codex.wordpress.org/Function_Reference/attribute_escape) por [`esc_attr`](https://codex.wordpress.org/Function_Reference/esc_attr). Consulte [Data_Validation](https://codex.wordpress.org/Data_Validation#Attribute_Nodes) para obter mais informações.

#### Suporte de tradução/I18n

[Para garantir uma transição suave para a localização do idioma, use as funções i18n](https://codex.wordpress.org/I18n_for_WordPress_Developers) baseadas em gettext do WordPress para agrupar todo o texto traduzível nos arquivos de modo. Isso torna mais fácil para os arquivos de tradução conectarem e traduzirem os rótulos, títulos e outos textos de modelo para o idioma atual do site. Veja mais em [WordPress Localization](https://codex.wordpress.org/WordPress_Localization) e [I18n for WordPress Developers](https://codex.wordpress.org/I18n_for_WordPress_Developers).

#### Classes temáticas

Implemente as seguintes tags de template para adicionar atributos de classe gerados pelo WordPress aos elementos body, post e comment. Para classes de postaagem, aplique apenas a elementos dentro do [The Loop](https://codex.wordpress.org/The_Loop).

- [`body_class()`](https://codex.wordpress.org/Function_Reference/body_class)
- [`post_class()`](https://codex.wordpress.org/Function_Reference/post_class)
- [`comment_class()`](https://codex.wordpress.org/Function_Reference/comment_class)

### Lista de verificação de arquivo de template

Ao desenvolver um tema, verifique seus arquivos de template em relação aos seguintes padrões de arquivo de template.

#### Cabeçalho do documento (header.php)
- [Use o DOCTYPE](http://en.wikipedia.org/wiki/Document_Type_Declaration) adequado
- A tag de abertura `<html>` deve incluir [`language_attributes()`](https://codex.wordpress.org/Function_Reference/language_attributes)
- O elemento charset `<meta>` deve ser colocado antes de tudo, incluindo o elemento `<title>`
- Use [`bloginfo()`](https://codex.wordpress.org/Function_Reference/bloginfo) para definir o conjunto de caracteres `<meta>` e os elementos de descrição
- Use [`wp_title()`](https://codex.wordpress.org/Function_Reference/wp_title) para definir o elemento `<title>`. [Veja o porquê](https://codex.wordpress.org/Function_Reference/wp_title#Note)
- Use links de [feed automáticos](https://codex.wordpress.org/Automatic_Feed_Links) para adicionar links de feed
- Adicione uma chamada para [wp_head()](https://codex.wordpress.org/Function_Reference/wp_head) antes da tag de fechamento `</head>`. Os plugins usam esse [gancho de ação](https://codex.wordpress.org/Plugin_API/Action_Reference) para adicionar seus próprios scripts, folhas de estilo e outras funcionalidades.
- Não vincule as folhas de estilo do tema no modelo de cabeçalho. Em vez disso, use o gancho de ação [`wp_enqueue_scripts` em uma função de tema](https://codex.wordpress.org/Plugin_API/Action_Reference/wp_enqueue_scripts)

Aqui está um exemplo de uma área de cabeçalho compatível com HTML5 formatada corretamente:

```php
<!DOCTYPEhtml>
<html <?php language_attributes(); ?>>
    <cabeça>
        <meta charset="<?php bloginfo( 'charset' ); ?>" />
        <title><?php wp_title(); ?></título>
        <link rel="profile" href="http://gmpg.org/xfn/11" />
        <link rel="pingback" href="<?php bloginfo( 'pingback_url' ); ?>" />
        <?php if ( is_singular() && get_option( 'thread_comments' ) ) wp_enqueue_script( 'comment-reply' ); ?>
        <?php wp_head(); ?>
    </head>
```

#### Menus de navegação (header.php)

- Navegação principal do Tema deve suportar um menu personalizado com [`wp_nav_menu()`](https://codex.wordpress.org/Function_Reference/wp_nav_menu)
  - Os menus devem suportar títulos de links longos e uma grande quantidade de itens de lista. Esses itens não devem quebrar o design ou o layout.
  - Os itens do submenu devem ser exibidos corretamente. Se possível, suporte estilos de menu suspenso para itens de submenu. Listas suspensas que permite mostrar a profundidade do menu em vez de apenas mostrar o nível superior.

#### Widgets (sidebar.php)
- O tema deve ser widgetizado o máximo possível. Qualquer área do layout que funcione como um widget (tag cloud, blogroll, lista de categorias) ou possa aceitar à barra lateral deve permitir widgets.
- O conteúdo que aparece em áreas com widgets por padrão (codificado na barra lateral, por exemplo) deve desaparecer quando os widgets são ativados em "Aparência > Widgets".

#### Rodapé (footer.php)

- Use a chamada [`wp_footer()`](https://codex.wordpress.org/Function_Reference/wp_footer), para aparecer logo antes de fechar a tag `body`.

```php
<?php wp_footer(); ?>
</body>
</html>
```

#### Índice (index.php)

- Exiba uma lista de postagens em formato de trecho ou completo. Escolha um ou outro conforme apropriado.
- Inclua [`wp_link_pages()`](https://codex.wordpress.org/Function_Reference/wp_link_pages) para oferecer suporte a links de navegação nas postagens.
