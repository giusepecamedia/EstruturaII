  public static void main(String[] args) {

    //== Teste agenda ==

    Exercicio2 arvoreAgenda = new Exercicio2();

    Agenda[] contatos = {

      new Agenda("Lucas", "Rua A, 123", "1111-1111"),

      new Agenda("Amanda", "Rua B, 456", "2222-2222"),

      new Agenda("Bruno", "Rua C, 789", "3333-3333"),

      new Agenda("Carla", "Rua D, 202", "4444-4444"),

    };

    for (Agenda contato : contatos) {

      arvoreAgenda.inserir(contato);

    }

    System.out.println("=== Contatos na Agenda ===");

    arvoreAgenda.emOrdem();



    // Buscar pessoa

    String nomeBuscaAgenda = "Helena";

    Agenda resultadoAgenda = arvoreAgenda.buscarPorNome(nomeBuscaAgenda);

    System.out.println("\nBusca na agenda: " + (resultadoAgenda != null ? resultadoAgenda : "Contato não encontrado"));

  }

}



class Agenda {

  String nome;

  String endereco;

  String telefone;



  public Agenda(String nome, String endereco, String telefone) {

    this.nome = nome;

    this.endereco = endereco;

    this.telefone = telefone;

  }



  @Override

  public String toString() {

    return nome + " - " + endereco + " - " + telefone;

  }

}



class Exercicio2 {

  private class No {

    Agenda contato;

    No esquerda, direita;



    No(Agenda contato) {

      this.contato = contato;

    }

  }



  private No raiz;



  public void inserir(Agenda contato) {

    raiz = inserirRec(raiz, contato);

  }



  private No inserirRec(No atual, Agenda contato) {

    if (atual == null) return new No(contato);



    if (contato.nome.compareToIgnoreCase(atual.contato.nome) < 0)

      atual.esquerda = inserirRec(atual.esquerda, contato);

    else if (contato.nome.compareToIgnoreCase(atual.contato.nome) > 0)

      atual.direita = inserirRec(atual.direita, contato);



    return atual;

  }



  public void emOrdem() {

    emOrdemRec(raiz);

  }



  private void emOrdemRec(No atual) {

    if (atual != null) {

      emOrdemRec(atual.esquerda);

      System.out.println(atual.contato);

      emOrdemRec(atual.direita);

    }

  }



  public Agenda buscarPorNome(String nome) {

    return buscarPorNomeRec(raiz, nome);

  }



  private Agenda buscarPorNomeRec(No atual, String nome) {

    if (atual == null) return null;



    int cmp = nome.compareToIgnoreCase(atual.contato.nome);

    if (cmp == 0) return atual.contato;

    else if (cmp < 0) return buscarPorNomeRec(atual.esquerda, nome);

    else return buscarPorNomeRec(atual.direita, nome);

  }

}
