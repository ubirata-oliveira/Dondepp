# 📍 Dondepp

**Dondepp** é um aplicativo Android que ajuda você a encontrar lugares próximos da sua localização, como farmácias, restaurantes, cafés, supermercados e hospitais. Com integração direta ao Uber, você pode solicitar uma viagem para o destino escolhido com apenas um toque.

---

## 🚀 Funcionalidades

- 🗺️ **Mapa Interativo**: Visualize sua localização e os lugares próximos em um mapa OpenStreetMap
- 🔍 **Busca por Categorias**: Encontre rapidamente farmácias, restaurantes, cafés, supermercados e hospitais
- ✍️ **Busca por Texto Livre**: Digite o nome de qualquer lugar e encontre opções próximas
- 📏 **Ordenação por Distância**: Resultados organizados automaticamente do mais próximo ao mais distante
- 📌 **Marcadores no Mapa**: Visualize todos os lugares encontrados com pins coloridos
- 📱 **Interface Intuitiva**: Bottom sheet deslizante com lista de resultados

### 🚧 Em Construção
- 🚗 **Integração com Aplicativos de Navegação**: Redirecionamento para Uber, Waze, Google Maps (em desenvolvimento)

---

## 🛠️ Tecnologias Utilizadas

### **Linguagem**
- Java

### **Bibliotecas Principais**
- **OSMDroid** (6.1.18) - Mapas OpenStreetMap
- **Retrofit** (2.9.0) - Requisições HTTP
- **Gson** (2.10.1) - Parsing JSON
- **Google Play Services Location** (21.0.1) - Geolocalização GPS
- **Material Design** (1.11.0) - Componentes visuais modernos
- **RecyclerView & CardView** - Listas e cards

### **APIs Externas**
- **Overpass API** - Busca de lugares no OpenStreetMap
- **Uber Deep Links** (em desenvolvimento) - Integração com aplicativo Uber
- **Intents Android** (em desenvolvimento) - Integração com Waze, Google Maps

---

## 📋 Pré-requisitos

- Android Studio Arctic Fox ou superior
- SDK Android 24 (Android 7.0) ou superior
- Dispositivo Android ou Emulador com:
    - GPS ativado
    - Conexão com internet (Wi-Fi ou dados móveis)
    - App Uber instalado (opcional - funciona via web se não instalado)

---

## 🔧 Instalação e Configuração

### **1. Clone o Repositório**

```bash
git clone https://github.com/Ubirata-Rodrigues/Dondepp.git
cd Dondepp
```

### **2. Abra no Android Studio**

1. Abra o Android Studio
2. Clique em `File` → `Open`
3. Selecione a pasta do projeto
4. Aguarde o Gradle sincronizar

### **3. Configure as Permissões**

O projeto já vem configurado com as permissões necessárias no `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

### **4. Execute o Projeto**

1. Conecte um dispositivo Android ou inicie um emulador
2. Clique em `Run` (▶️) ou pressione `Shift + F10`
3. Aguarde a instalação
4. Permita o acesso à localização quando solicitado

---

## 📱 Como Usar

### **Passo 1: Permita o Acesso à Localização**
Ao abrir o app pela primeira vez, conceda permissão de localização para que o app possa encontrar lugares próximos.

### **Passo 2: Escolha uma Categoria**
Toque em um dos botões de categoria:
- 🏥 **Farmácias**
- 🍽️ **Restaurantes**
- ☕ **Cafés**
- 🛒 **Supermercados**
- 🏨 **Hospitais**

### **Passo 3: Visualize os Resultados**
- A lista aparecerá no bottom sheet (parte inferior)
- Os lugares também serão marcados no mapa com pins
- Resultados ordenados por distância (mais próximo primeiro)

### **Passo 4: Navegação (Em Desenvolvimento)**
> ⚠️ **Funcionalidade em construção**: A integração com apps de navegação (Uber, Waze, Google Maps) será implementada em breve.

### **Passo 5: Busca Personalizada**
- Digite o nome de um lugar no campo de busca
- Pressione Enter ou clique na lupa 🔍
- Veja os resultados que correspondem à sua busca

---

## 🏗️ Arquitetura do Projeto

```
app/src/main/java/com.seuprojeto.localfinder/
│
├── MainActivity.java                 # Activity principal
│
├── models/                           # Modelos de dados
│   ├── Place.java                    # Representa um lugar
│   └── OverpassResponse.java         # Resposta da API Overpass
│
├── adapters/                         # Adapters do RecyclerView
│   └── PlacesAdapter.java            # Adapter da lista de lugares
│
├── services/                         # Serviços de API
│   └── OverpassService.java          # Interface Retrofit para Overpass API
│
└── utils/                            # Utilitários
    └── LocationHelper.java           # Gerenciamento de GPS e localização

app/src/main/res/
│
├── layout/
│   ├── activity_main.xml             # Layout da tela principal
│   └── item_place.xml                # Layout de cada item da lista
│
└── values/
    ├── strings.xml
    ├── colors.xml
    └── themes.xml
```

---

## 🔍 Como Funciona

### **1. Obtenção da Localização**
O app usa o **Google Play Services Location** para obter a localização GPS do usuário em tempo real.

### **2. Busca de Lugares**
Quando o usuário seleciona uma categoria:
1. O app monta uma query no formato Overpass QL
2. Envia requisição HTTP para `https://overpass-api.de/api/`
3. A API retorna um JSON com lugares próximos (raio de 2km)

**Exemplo de Query:**
```
[out:json];
(
  node["amenity"="pharmacy"](around:2000,-15.7942,-47.8822);
  way["amenity"="pharmacy"](around:2000,-15.7942,-47.8822);
);
out center;
```

### **3. Processamento dos Dados**
1. Converte JSON → objetos Java (`Place`)
2. Calcula distância de cada lugar usando fórmula Haversine
3. Ordena por proximidade
4. Exibe na lista e adiciona marcadores no mapa

### **4. Integração com Aplicativos de Navegação (Em Desenvolvimento)**
> 🚧 **Funcionalidade planejada**: Integração com Uber, Waze e Google Maps para navegação até o destino escolhido.

---

## 🎨 Capturas de Tela

> ⚠️ Adicione screenshots do seu app aqui após concluir o projeto

```markdown
![Tela Principal](screenshots/main_screen.png)
![Busca de Farmácias](screenshots/pharmacy_search.png)
![Lista de Resultados](screenshots/results_list.png)
```

---

## 🐛 Problemas Conhecidos

- **GPS em Emulador**: A localização pode ser imprecisa. Recomendamos testar em dispositivo real.
- **API Overpass**: Às vezes pode estar lenta ou sobrecarregada. Se não retornar resultados, tente novamente.

### 🚧 Funcionalidades em Desenvolvimento
- **Integração com Apps de Navegação**: Redirecionamento para Uber, Waze e Google Maps (planejado para próxima versão)

---

## 📚 Referências

- [OSMDroid Documentation](https://github.com/osmdroid/osmdroid)
- [Overpass API](https://wiki.openstreetmap.org/wiki/Overpass_API)
- [Retrofit Documentation](https://square.github.io/retrofit/)
- [OpenStreetMap](https://www.openstreetmap.org/)
- [Uber Deep Links](https://developer.uber.com/docs/riders/ride-requests/tutorials/deep-links/introduction)

---

## 📄 Licença

Este projeto foi desenvolvido para fins educacionais.

---

## 👥 Equipe de Desenvolvimento

Este é um projeto acadêmico desenvolvido como trabalho final da disciplina de Java Mobile.

| Nome                   | GitHub                                                     | LinkedIn                                                                                        |
|------------------------|------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| **[Ubiratã Rodrigues]**  | [@Ubirata-Rodrigues](https://github.com/Ubirata-Rodrigues) | [linkedin.com/in/perfil](https://linkedin.com/in/ubirata-oliveira)                                        |
| **[Paulo G M Santos]** | [@paulogm15](https://github.com/paulogm15)                 | [linkedin.com/in/paulogm](https://www.linkedin.com/in/paulo-gabriel-mendes-dos-santos-a81650106/) |


---

## 🙏 Agradecimentos

- Professor Kristian Pablo Dias Pacheco pela orientação
- OpenStreetMap pela API gratuita e dados abertos
- Comunidade OSMDroid pelo excelente framework
- Colegas de turma pelo apoio durante o desenvolvimento

---

## 📝 Notas de Versão

### **v1.0.0** (Data)
- ✨ Lançamento inicial
- 🗺️ Mapa interativo com OSMDroid
- 🔍 Busca por categorias (farmácia, restaurante, café, supermercado, hospital)
- ✍️ Busca por texto livre
- 📏 Ordenação por distância
- 📱 Interface responsiva com Bottom Sheet

### **🚧 Próximas Versões**
- 🚗 Integração com Uber
- 🗺️ Integração com Waze e Google Maps
- ⭐ Sistema de favoritos
- 📜 Histórico de buscas

---

**Desenvolvido com ❤️ como projeto final de Java Mobile** 
