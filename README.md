# Práctica de Docker con Apache

## 1. Comproba que a tes a imaxe httpd :
En primeiro lugar, debes comprobar se tes a imaxe de Apache (httpd) no teu ordenador. Para iso, executa imaxes docker e comproba se aparece a imaxe httpd. Se non o tes, podes descargalo co comando 'docker pull httpd'.


## 2. Crea un contenedor de nome 'asir_httpd' :
Para crear un contedor chamado 'asir_httpd' e asignarlle o porto 8080 ao 80: Unha vez que teñas descargada a imaxe, podes crear un contedor chamado asir_httpd. Neste contedor, o porto 80 estará vinculado co porto 8080 da túa máquina, o que se fai executando o seguinte comando: docker run -d --name asir_httpd -p 8080:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd. Con este comando, o directorio local htdocs quedará montado dentro do contedor no directorio htdocs de Apache, permitindo que os ficheiros que teñas no teu equipo poidan verse no servidor web.


## 3. Mapea o porto 80 do contenedor có 8080 da túa máquina. Utiliza bind mount para que o directorio do apache2 'htdocs' estea montado nun directorio da túa elección.Utiliza -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ :
O montaxe de volumes faise empregando a opción -v, que neste caso conecta o directorio local "$PWD"/htdocs co directorio htdocs dentro do contedor (/usr/local/apache2/htdocs/). Isto permite que poidas xestionar os teus arquivos web desde o teu ordenador local, que logo serán servidos polo contedor de Apache. Hai que asegurarse  de que o directorio local htdocs conteña unha páxina HTML, como un ficheiro index.html, para poder acceder a ela dende o servidor web.


## 4. Mostra unha páxina html aloxada no apache2 dende o teu navegador:
A continuación, abre o teu navegador e vai á dirección http://localhost:8080 para comprobar que a páxina HTML se está servindo correctamente. Se todo está ben configurado, debería ver a páxina que creei no  directorio local co mensaxe que puxen dentro da páxina.


## 5. Crea un contenedor 'asir_web1' que use este mesmo directorio para 'htdocs' e o puerto 8000:
A continuación, crea outro contedor chamado asir_web1, que empregue o mesmo directorio local para htdocs e que estea mapeado ao porto 8000. Isto faise executando o comando: docker run -d --name asir_web1 -p 8000:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd. Agora, o contedor asir_web1 utilizará o mesmo directorio local para os arquivos web, pero servirá as páxinas no porto 8000 en vez do 8080.


## 6.Crea outro contenedor 'asir_web2' có el mesmo directorio e otro puerto, como o 8090. Comproba que os dous servidores mostran a mesma páxina:
Finalmente, crea un terceiro contedor chamado asir_web2, utilizando tamén o mesmo directorio local para htdocs, pero mapeando o porto 8090. Isto faise co comando: docker run -d --name asir_web2 -p 8090:80 -v "$PWD"/htdocs:/usr/local/apache2/htdocs/ httpd. Agora teremos tres contedores que están a servir a mesma páxina HTML, pero en diferentes portos: 8080, 8000 e 8090.
Para verificar que os tres servidores están a funcionar correctamente e están a mostrar a mesma páxina, abre o teu navegador e accede a http://localhost:8000 e http://localhost:8090. Ambos servidores deberían amosar a mesma páxina HTML, xa que están a empregar o mesmo volume montado para os arquivos web.
