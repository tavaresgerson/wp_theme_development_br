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

Vejamos os vários modelos que podem ser definidos como parte de um tema
