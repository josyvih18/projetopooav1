class Livro {
  constructor(titulo, autor, genero, anoPublicacao, sinopse) {
    this.titulo = titulo;
    this.autor = autor;
    this.genero = genero;
    this.anoPublicacao = anoPublicacao;
    this.sinopse = sinopse;
  }
}

class Biblioteca {
  constructor() {
    this.livros = [];
  }

  adicionarLivro(livro) {
    this.livros.push(livro);
    console.log('Livro adicionado com sucesso.');
  }

  pesquisarLivros(termo) {
    return this.livros.filter(livro =>
      Object.values(livro).some(valor => valor.includes(termo))
    );
  }

  editarLivro(index, novoLivro) {
    this.livros[index] = novoLivro;
    console.log('Livro editado com sucesso.');
  }

  excluirLivro(index) {
    this.livros.splice(index, 1);
    console.log('Livro excluído com sucesso.');
  }
}

const biblioteca = new Biblioteca();

function exibirMenu() {
  console.log('Escolha uma opção:');
  console.log('1. Adicionar Livro');
  console.log('2. Pesquisar Livros');
  console.log('3. Editar Livro');
  console.log('4. Excluir Livro');
  console.log('5. Sair');
  
  const escolha = parseInt(prompt('Digite o número da opção desejada:'));

  switch (escolha) {
    case 1: {
      const novoLivro = new Livro(
        prompt('Título:'),
        prompt('Autor:'),
        prompt('Gênero:'),
        parseInt(prompt('Ano de Publicação:')),
        prompt('Sinopse:')
      );
      biblioteca.adicionarLivro(novoLivro);
      break;
    }
    case 2: {
      const termo = prompt('Termo de Pesquisa:');
      const resultados = biblioteca.pesquisarLivros(termo);
      resultados.forEach((livro, index) => {
        console.log(`${index + 1}. ${livro.titulo} - ${livro.autor}`);
      });
      break;
    }
    case 3: {
      const index = parseInt(prompt('Índice do Livro a Editar:')) - 1;
      const novoLivro = new Livro(
        prompt('Novo Título:'),
        prompt('Novo Autor:'),
        prompt('Novo Gênero:'),
        parseInt(prompt('Novo Ano de Publicação:')),
        prompt('Nova Sinopse:')
      );
      biblioteca.editarLivro(index, novoLivro);
      break;
    }
    case 4: {
      const index = parseInt(prompt('Índice do Livro a Excluir:')) - 1;
      biblioteca.excluirLivro(index);
      break;
    }
    case 5:
      console.log('Saindo da aplicação.');
      return;
    default:
      console.log('Opção inválida.');
  }

  exibirMenu();
}

exibirMenu();
