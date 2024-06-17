import csv

class Artista:
    def __init__(self, nome, data_nascimento, local_nascimento, biografia, estilos):
        self.nome = nome
        self.data_nascimento = data_nascimento
        self.local_nascimento = local_nascimento
        self.biografia = biografia
        self.estilos = estilos  # lista de estilos associados ao artista

class EstiloArtistico:
    def __init__(self, denominacao, periodo, caracteristicas, escola):
        self.denominacao = denominacao
        self.periodo = periodo
        self.caracteristicas = caracteristicas
        self.escola = escola

class ObraDeArte:
    def __init__(self, titulo, data_criacao, tema, estilo, descricao, tecnica, autor, localizacao):
        self.titulo = titulo
        self.data_criacao = data_criacao
        self.tema = tema
        self.estilo = estilo
        self.descricao = descricao
        self.tecnica = tecnica
        self.autor = autor
        self.localizacao = localizacao
        self.documentos = []  # lista de documentos associados
        self.figura_historica = None  # figura histórica associada, se houver

class Documento:
    def __init__(self, tipo, descricao):
        self.tipo = tipo
        self.descricao = descricao

class FiguraHistorica:
    def __init__(self, nome, descricao):
        self.nome = nome
        self.descricao = descricao

class Emprestimo:
    def __init__(self, obra, periodo_emprestimo, nome_evento, responsavel, tema):
        self.obra = obra
        self.periodo_emprestimo = periodo_emprestimo
        self.nome_evento = nome_evento
        self.responsavel = responsavel
        self.tema = tema

class VisitaGuiada:
    def __init__(self, tema, descricao, obras):
        self.tema = tema
        self.descricao = descricao
        self.obras = obras  # lista de obras na visita guiada

# Exemplo de uso
# Criando um artista
artista1 = Artista("Leonardo da Vinci", "15/04/1452", "Vinci, Itália",
                   "Leonardo da Vinci foi um dos maiores artistas do Renascimento...",
                   ["Renascimento", "Alta Renascença"])

# Criando um estilo artístico
estilo1 = EstiloArtistico("Renascimento", "Séculos XIV a XVII",
                          "Valorização da razão, ciência e humanismo. Uso de perspectiva e naturalismo.",
                          "Escola Florentina")

# Criando uma obra de arte
obra1 = ObraDeArte("Mona Lisa", "1503-1506", "Retrato", estilo1, "A Mona Lisa é um retrato renascentista famoso...",
                   "Óleo sobre madeira", artista1, "Sala 4, Ala A")

# Associando um documento à obra
documento1 = Documento("Fotografia", "Fotografia da Mona Lisa durante restauração")
obra1.documentos.append(documento1)

# Criando uma figura histórica associada à obra
figura1 = FiguraHistorica("Lisa Gherardini", "Lisa Gherardini foi uma nobre florentina, esposa de Francesco del Giocondo...")
obra1.figura_historica = figura1

# Registrar empréstimo de obra
emprestimo1 = Emprestimo(obra1, "01/07/2024 - 15/08/2024", "Exposição Internacional de Artes", "Curador X",
                         "Retratos Renascentistas")

# Criar uma visita guiada
visita_guiada1 = VisitaGuiada("O Renascimento em Florença", "Descubra o movimento artístico que transformou a arte europeia...",
                              [obra1])

# Exemplo de ordenação de obras por título
obras = [obra1]
obras.sort(key=lambda x: x.titulo)

# Escrever informações em arquivos (exemplo usando CSV)
def salvar_obras_csv(obras, nome_arquivo):
    with open(nome_arquivo, mode='w', newline='', encoding='utf-8') as file:
        writer = csv.writer(file)
        writer.writerow(["Título", "Data de Criação", "Tema", "Estilo", "Descrição", "Técnica", "Autor", "Localização"])
        for obra in obras:
            writer.writerow([obra.titulo, obra.data_criacao, obra.tema, obra.estilo.denominacao,
                             obra.descricao, obra.tecnica, obra.autor.nome, obra.localizacao])

# Exemplo de leitura de informações de arquivos (para implementar leitura, expandir esta função)

# Tratamento de exceções
try:
    # Código que pode gerar exceções
    pass
except FileNotFoundError:
    print("Arquivo não encontrado.")
except Exception as e:
    print(f"Ocorreu um erro: {e}")

# Exemplo de utilização
if __name__ == "__main__":
    # Exemplos de uso das funcionalidades definidas acima
    salvar_obras_csv([obra1], "obras.csv")
