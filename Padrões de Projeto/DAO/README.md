# PADRÃO DE PROJETO DAO

## Sumário
1. **Materiais**
2. **Definição**
3. **Arquitetura**
4. **Responsabilidades**
5. **Implementação**
6. **Mais Informações**
7. **Referências**

<br>

## 1. **Materiais**

Este conteúdo está estruturado da seguinte forma:

- **Documentos**
    - Conteúdo em arquivo .docx e .pdf

- **Imagens**
    - Imagens dos diagramas
    
- **README.MD**
    - Arquivo MARKDOWN para melhor visualização do conteúdo

<br>

## 2. **Definição**

<p align="justify">
O Data Access Object (DAO) é um padrão de projetos onde um objeto:
</p>

- Provê uma interface que abstrai o acesso a dados;
- Lê e grava a partir da origem de dados (banco de dados, arquivo, memória, etc.);
- Encapsula o acesso aos dados, de forma que as demais classes não precisam saber sobre isso.

<br>

## 3. **Arquitetura**

<p align="justify">
Numa aplicação web comum seguindo o modelo MVC, os DAOs ficam junto com o Model fazendo um trabalho de suporte, integrando a fonte de dados ao modelo de objetos do sistema.
</p>

![DIAGRAMA-MVC](/Padr%C3%B5es%20de%20Projeto/DAO/Imagens/Diagrama-DAO.png)

<br>

## 4. **Responsabilidades**

<p align="justify">
Seguindo o princípio de responsabilidade única, um DAO não deve ser responsável por mais do que acesso aos dados.

Definir quem faz o que pode ser um problema quando pensamos na arquitetura de um sistema, mas grande parte disso é porque misturamos as coisas.

Se olhar bem o diagrama acima, fica fácil identificarmos a responsabilidade de cada elemento.
Suponha que o usuário está acessando a página inicial do sistema web. Então uma interação comum poderia ser:
</p>

- Um controller recebe a requisição do usuário
- Esse controller chama o método do service adequado para obter as informações para aquela página
- O service chama um ou mais métodos de DAOs para obter as informações necessárias e retorna os dados para o controller
- O controller recebe os dados e redireciona o usuário para uma view que vai renderizar o HTML da página

<p align="justify">
Adicionalmente, temos que:
</p>

- Controllers executam lógica relacionada à navegação do usuário no sistema, isto é, qual URL ou qual ação exibe qual página
- Services executam a lógica do sistema, que pode incluir gerenciar transações e processar os dados

<p align="justify">
Portanto, em geral, cada método do DAO deve fazer uma única leitura ou gravação no banco de dados e não deve controlar transações ou realizar operações adicionais, tal como realizar alterações nos dados recebidos do serviço.
</p>

<br>

## 5. **Implementação**

<p align="justify">
A vantagem de usar uma classe específica para o acesso a dados é evitar espalhar SQLs em todo lugar, tornando a manutenção e evolução de um sistema um pesadelo.

Em geral, agrupa-se os acessos aos dados por similaridade, por exemplo, uma classe por tabela. Porém, não é sempre que isso faz sentido, principalmente quando o sistema não é somente feito de cadastros simples (CRUD).

Um exemplo claro são sistemas que possuem buscas avançadas em que acessam várias tabelas. Nesse caso, cada situação precisa ser analisada caso a caso. No exemplo das buscas, um DAO específico para isso seria interessante.

Usar interfaces é opcional. Veja, Java tem uma péssima reputação por usar muitas interfaces, mas isso tem seus motivos, por exemplo:
</p>

- Permitir várias implementações para bancos de dados diferentes sem alterar o sistema
- Permitir versões diferentes convivendo na mesma versão do sistema (isso pode ser útil em alguns casos, como quando algum campo pode ou não existir e você quer atualizar o sistema sem obrigar a criação do campo)
- Facilitar testes unitários criando implementações Fakes dos DAOs, por exemplo, que usam listas em memória, embora frameworks como - Mockito consigam gerar mocks dinamicamente sem uma interface.

<br>

## 6. **Mais Informações**

<p align="justify">
Saiba mais sobre o padrão de projeto DAO nos seguintes sites:
Explicações:
</p>

- [Argo Navis](http://www.argonavis.com.br/cursos/java/j550/j550_13.pdf)
- [FACOM](http://www.facom.ufu.br/~bacala/PI/11-WebMVCePatterns.pdf)

<p align="justify">
Explicações com Implementação:
</p>

- [DEINF/CCET](http://www.deinf.ufma.br/~geraldo/poo/10.1.DAO.pdf)
- [DevMedia](https://www.devmedia.com.br/implementando-o-data-access-object-no-javaee/33339)
- [Macoratti](http://www.macoratti.net/11/10/pp_dao1.htm#:~:text=O%20padr%C3%A3o%20DAO%20%C3%A9%20um,utilizam%20banco%20de%20dados%20relacionais)

<br>

## 7. **Referências**

Link do site utilizado para a criação do conteúdo.

- [Stack Overflow](https://pt.stackoverflow.com/questions/113840/como-funciona-o-padr%C3%A3o-dao)