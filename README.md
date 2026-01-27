# 📱 Client Control - Controle de Clientes

![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white)

Aplicativo Flutter para gerenciamento de clientes e seus respectivos tipos, desenvolvido como parte do curso de Gerenciamento de Estados Complexos da Alura.

![Thumbnail GitHub](./thumb.png)

## 📸 Screenshot do App

<p align="center">
  <img src="./screenshot.png" alt="Screenshot do Client Control" width="300">
</p>

---

## 📋 Sobre o Projeto

O **Client Control** é uma aplicação mobile desenvolvida em Flutter que permite o gerenciamento completo de clientes e categorias de clientes. O projeto foi desenvolvido durante o curso **"Flutter: gerenciamento de estados com Provider"** da Alura, como parte da **Imersão Digital Santander 2025 - Desenvolvimento Mobile**. A aplicação demonstra conceitos avançados de gerenciamento de estados em Flutter, oferecendo uma interface intuitiva para cadastro, visualização e exclusão de registros.

### ✨ Funcionalidades Principais

- ✅ **Cadastro de Clientes**: Adicione novos clientes com nome, email e tipo
- ✅ **Cadastro de Tipos**: Crie categorias personalizadas de clientes com ícones
- ✅ **Listagem Dinâmica**: Visualize todos os clientes e tipos cadastrados
- ✅ **Exclusão por Deslize**: Remova registros com gesto de swipe (Dismissible)
- ✅ **Seletor de Ícones**: Escolha ícones personalizados para cada tipo de cliente
- ✅ **Navegação Fluida**: Menu hamburguer para navegação entre telas
- ✅ **Interface Moderna**: Design Material com cores personalizadas

---

## 🏗️ Arquitetura do Projeto

```
lib/
├── main.dart                      # Ponto de entrada da aplicação com MultiProvider
├── components/
│   ├── hamburger_menu.dart        # Menu lateral de navegação
│   └── icon_picker.dart           # Componente de seleção de ícones
├── models/
│   ├── client.dart                # Model de Cliente
│   ├── clients.dart               # Gerenciador de estado dos Clientes com ChangeNotifier
│   ├── client_type.dart           # Model de Tipo de Cliente
│   └── types.dart                 # Gerenciador de estado dos Tipos com ChangeNotifier
└── pages/
    ├── clients_page.dart          # Tela de gerenciamento de clientes
    └── client_types_page.dart     # Tela de gerenciamento de tipos
```

### 📦 Models e Gerenciamento de Estado

#### Client (Cliente)
```dart
- name: String          // Nome do cliente
- email: String         // Email do cliente
- type: ClientType      // Tipo/categoria do cliente
```

#### Clients (Gerenciador de Clientes) - ChangeNotifier
```dart
- clients: List<Client>  // Lista de clientes
- add(Client): void      // Adiciona um cliente e notifica listeners
- extends ChangeNotifier // Notifica listeners sobre mudanças
```

#### ClientType (Tipo de Cliente)
```dart
- name: String          // Nome do tipo
- icon: IconData?       // Ícone representativo
```

#### Types (Gerenciador de Tipos) - ChangeNotifier
```dart
- types: List<ClientType>  // Lista de tipos de clientes
- add(ClientType): void    // Adiciona um tipo e notifica listeners
- extends ChangeNotifier   // Notifica listeners sobre mudanças
```

---

## 🔄 Gerenciamento de Estado com Provider

Este projeto utiliza o **Provider** como solução de gerenciamento de estado, implementando o padrão **ChangeNotifier** para notificar as telas sobre mudanças nos dados.

### Configuração do Provider

O Provider é configurado no ponto de entrada da aplicação ([main.dart](lib/main.dart)) utilizando **MultiProvider** para gerenciar múltiplos estados:

```dart
void main() {
  runApp(MultiProvider(
    providers: [
      ChangeNotifierProvider(
        create: (context) => Clients(clients: [])
      ),
      ChangeNotifierProvider(
        create: (context) => Types(types: [
          ClientType(name: 'Platinum', icon: Icons.credit_card),
          ClientType(name: 'Golden', icon: Icons.card_membership),
          ClientType(name: 'Titanium', icon: Icons.credit_score),
          ClientType(name: 'Diamond', icon: Icons.diamond),
        ])
      ),
    ],
    child: const MyApp(),
  ));
}
```

### Uso do Consumer

As telas utilizam o widget **Consumer** para escutar mudanças e reagir automaticamente:

```dart
Consumer<Clients>(
  builder: (context, list, widget) {
    return ListView.builder(
      itemCount: list.clients.length,
      itemBuilder: (context, index) {
        // Renderiza cada cliente
      },
    );
  },
)
```

### Benefícios do Provider

- ✅ **Reatividade**: As telas são atualizadas automaticamente quando os dados mudam
- ✅ **Separação de Responsabilidades**: Lógica de negócio separada da UI
- ✅ **Performance**: Apenas widgets que dependem do estado são reconstruídos
- ✅ **Facilidade de Manutenção**: Código mais organizado e testável
- ✅ **Múltiplos Estados**: Gerenciamento independente de Clientes e Tipos

### Dependências

```yaml
dependencies:
  provider: ^6.0.3
```

---

## 🚀 Como Executar

### Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- **Flutter SDK**: Versão 2.16.2 ou superior
- **Dart SDK**: Versão 2.16.2 < 3.0.0
- **IDE**: Android Studio, VS Code ou IntelliJ IDEA
- **Emulador**: Android ou iOS, ou dispositivo físico conectado

### Instalação

1. **Clone o repositório**
```bash
git clone https://github.com/OYanEnrique/alura-flutter-clientes.git
cd alura-flutter-clientes
```

2. **Instale as dependências**
```bash
flutter pub get
```

3. **Verifique se há dispositivos disponíveis**
```bash
flutter devices
```

4. **Execute o aplicativo**
```bash
flutter run
```

### 🔧 Comandos Úteis

```bash
# Executar em modo debug
flutter run

# Executar em modo release
flutter run --release

# Limpar build
flutter clean

# Verificar dependências desatualizadas
flutter pub outdated

# Atualizar dependências
flutter pub upgrade

# Gerar APK
flutter build apk

# Gerar App Bundle (Android)
flutter build appbundle

# Executar testes
flutter test
```

---

## 🎨 Telas da Aplicação

### 1. Tela de Clientes
- Lista todos os clientes cadastrados
- Exibe nome, tipo e ícone associado
- Botão flutuante para adicionar novos clientes
- Gesto de deslize para excluir clientes

### 2. Tela de Tipos de Cliente
- Lista todos os tipos de clientes cadastrados
- Exibe nome e ícone de cada tipo
- Botão flutuante para adicionar novos tipos
- Gesto de deslize para excluir tipos
- Seletor de ícones personalizado

### 3. Menu Hamburguer
- Navegação entre as telas principais
- Acesso rápido a Clientes e Tipos

---

## 🎓 Conceitos de Gerenciamento de Estados

Este projeto foi desenvolvido para ensinar e demonstrar conceitos importantes de gerenciamento de estados em Flutter:

### Técnicas Abordadas

- **Provider**: Gerenciador de estados leve e eficiente
- **Consumer**: Widget para consumir estados reativamente
- **Provider.of**: Acesso a estados fora da árvore de widgets
- **ChangeNotifier**: Padrão de notificação de mudanças
- **notifyListeners()**: Notificação de alterações no estado
- **MultiProvider**: Gerenciamento de múltiplos providers
- **Single Source of Truth**: Única fonte da verdade para o estado
- **Redux Pattern**: Conceitos e princípios do Redux
- **BloC Pattern**: Teoria do padrão BloC (Business Logic Component)

### Estado Local vs Global

O projeto demonstra diferentes abordagens:
- **Estado Local**: Usando `StatefulWidget` e `setState()`
- **Estado Global**: Preparado para implementação com Provider
- **Passagem de Dados**: Entre widgets e telas

---

## 🛠️ Tecnologias e Dependências

### Dependências Principais

```yaml
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
```

### Dependências de Desenvolvimento

```yaml
dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^1.0.0
```

### Plataformas Suportadas

- ✅ Android
- ✅ iOS
- ⚠️ Web (requer adaptações)
- ⚠️ Desktop (requer adaptações)

---

## 📱 Widgets e Componentes Utilizados

### Widgets do Material Design

- `Scaffold`: Estrutura básica das telas
- `AppBar`: Barra superior com título
- `Drawer`: Menu lateral hamburguer
- `ListView.builder`: Listas dinâmicas e performáticas
- `FloatingActionButton`: Botão de ação flutuante
- `AlertDialog`: Diálogos modais para cadastro
- `TextFormField`: Campos de entrada de texto
- `DropdownButton`: Seletor dropdown para tipos
- `Dismissible`: Widget para exclusão por deslize
- `ListTile`: Item de lista com ícone e texto
- `ElevatedButton`: Botões elevados
- `TextButton`: Botões de texto

### Componentes Customizados

- `HamburgerMenu`: Menu de navegação lateral
- `IconPicker`: Seletor de ícones personalizados

---

## 🎯 Funcionalidades Detalhadas

### Cadastro de Cliente

1. Clique no botão flutuante (+) na tela de Clientes
2. Preencha o nome do cliente
3. Preencha o email do cliente
4. Selecione o tipo no dropdown
5. Clique em "Salvar"

### Cadastro de Tipo

1. Navegue até "Tipos de cliente" pelo menu
2. Clique no botão flutuante (+)
3. Preencha o nome do tipo
4. Clique em "Selecionar ícone"
5. Escolha um ícone da galeria
6. Clique em "Salvar"

### Exclusão de Registros

- Deslize o item para a esquerda ou direita
- O item será removido automaticamente
- O fundo vermelho indica a ação de exclusão

---

## 🔄 Rotas da Aplicação

```dart
routes: {
  '/': (context) => ClientsPage(title: 'Clientes'),
  '/tipos': (context) => ClientTypesPage(title: 'Tipos de cliente'),
}
```

---

## 🎨 Tema e Cores

O aplicativo utiliza um tema personalizado com:

- **Cor primária**: Indigo (Clientes)
- **Cor secundária**: Deep Orange (Tipos)
- **Material Design**: Versão 2

---

## 📚 Recursos de Aprendizado

### O que você aprenderá:

1. **Fundamentos de Estado**
   - O que é estado em Flutter
   - Estado local vs estado global
   - Ciclo de vida de widgets stateful

2. **Gerenciamento com Provider**
   - Instalação e configuração
   - Criação de providers
   - Consumo de estados

3. **Padrões de Arquitetura**
   - Single Source of Truth
   - Separação de responsabilidades
   - Models e notificadores

4. **Boas Práticas**
   - Organização de código
   - Componentização
   - Reutilização de widgets

---

## 🐛 Problemas Conhecidos

- A lista de tipos está duplicada entre `clients_page.dart` e `client_types_page.dart`
- Não há persistência de dados (os dados são perdidos ao fechar o app)
- Não há validação de campos obrigatórios
- Typo nos botões: "Calcelar" deveria ser "Cancelar"

### Melhorias Futuras

- [ ] Implementar Provider para estado global
- [ ] Adicionar persistência com SQLite ou Shared Preferences
- [ ] Validação de formulários
- [ ] Edição de clientes e tipos existentes
- [ ] Busca e filtros
- [ ] Testes unitários e de widget
- [ ] Internacionalização (i18n)
- [ ] Modo escuro (Dark Mode)

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/MinhaFeature`)
3. Commit suas mudanças (`git commit -m 'Adiciona MinhaFeature'`)
4. Push para a branch (`git push origin feature/MinhaFeature`)
5. Abra um Pull Request

---

## 📄 Licença

Este projeto está sob a licença especificada no arquivo [LICENSE](LICENSE).

---

## 👨‍💻 Autor

**OYanEnrique**

Desenvolvido durante o curso **"Flutter: gerenciamento de estados com Provider"** da [Alura](https://www.alura.com.br/), como parte da **Imersão Digital Santander 2025 - Desenvolvimento Mobile**.

- GitHub: [@OYanEnrique](https://github.com/OYanEnrique)
- Repositório: [alura-flutter-clientes](https://github.com/OYanEnrique/alura-flutter-clientes)

---

## 📞 Suporte

Se você encontrar algum problema ou tiver dúvidas:

1. Verifique a documentação oficial do [Flutter](https://flutter.dev/docs)
2. Consulte os [issues do projeto](https://github.com/OYanEnrique/alura-flutter-clientes/issues)
3. Acesse o curso da Alura para mais detalhes

---

## 🌟 Agradecimentos

- **Santander** pela oportunidade através da Imersão Digital 2025
- **Alura** pelo excelente conteúdo educacional
- **Comunidade Flutter** pelo suporte e recursos
- **Google Flutter Team** pela framework incrível

---

**Feito com ❤️ e Flutter**

Esse curso faz parte da [formação de Flutter da Alura](https://cursos.alura.com.br/formacao-flutter)

