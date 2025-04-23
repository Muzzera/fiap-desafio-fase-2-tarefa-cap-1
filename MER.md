## 🧩 Modelo Entidade-Relacionamento (MER)

### 🧑 ENTIDADE: PRODUTOR
| Atributo      | Tipo         | Chave     |
|---------------|--------------|-----------|
| id_produtor   | NUMBER       | PK        |
| nome          | VARCHAR2(100)|           |
| email         | VARCHAR2(100)|           |
| telefone      | VARCHAR2(20) |           |

---

### 🌱 ENTIDADE: PLANTAÇÃO
| Atributo      | Tipo           | Chave     |
|---------------|----------------|-----------|
| id_plantacao  | NUMBER         | PK        |
| id_produtor   | NUMBER         | FK → Produtor |
| nome          | VARCHAR2(100)  |           |
| localizacao   | VARCHAR2(100)  |           |

**Relacionamento:** Um produtor pode ter várias plantações (1:N)

---

### 🪴 ENTIDADE: CULTURA
| Atributo      | Tipo            | Chave     |
|---------------|-----------------|-----------|
| id_cultura    | NUMBER          | PK        |
| nome_cultura  | VARCHAR2(100)   |           |
| descricao     | VARCHAR2(255)   |           |

---

### 📡 ENTIDADE: SENSOR
| Atributo        | Tipo            | Chave     |
|-----------------|-----------------|-----------|
| id_sensor       | NUMBER          | PK        |
| tipo_sensor     | VARCHAR2(50)    |           |
| modelo          | VARCHAR2(100)   |           |
| unidade_medida  | VARCHAR2(50)    |           |

---

### 📈 ENTIDADE: LEITURA_SENSOR
| Atributo        | Tipo            | Chave     |
|-----------------|-----------------|-----------|
| id_leitura      | NUMBER          | PK        |
| id_sensor       | NUMBER          | FK → Sensor |
| id_plantacao    | NUMBER          | FK → Plantacao |
| data_hora       | DATE            |           |
| valor_medido    | NUMBER          |           |

**Relacionamentos:**
- Um sensor pode gerar várias leituras (1:N)
- Uma plantação pode ter várias leituras (1:N)

---

### 💧 ENTIDADE: AJUSTE_APLICACAO
| Atributo            | Tipo          | Chave     |
|---------------------|---------------|-----------|
| id_ajuste           | NUMBER        | PK        |
| id_plantacao        | NUMBER        | FK → Plantacao |
| data_hora           | DATE          |           |
| tipo_aplicacao      | VARCHAR2(50)  |           |
| quantidade_aplicada | NUMBER        |           |

**Relacionamento:** Uma plantação pode ter vários ajustes de aplicação (1:N)

---

### 🌾 ENTIDADE: PLANTACAO_CULTURA (Relacionamento N:N)
| Atributo        | Tipo    | Chave               |
|-----------------|---------|---------------------|
| id_plantacao    | NUMBER  | PK, FK → Plantacao  |
| id_cultura      | NUMBER  | PK, FK → Cultura    |

**Relacionamento:** Uma plantação pode ter várias culturas e uma cultura pode estar em várias plantações (N:N via tabela associativa)

---

### 🔗 Resumo das Cardinalidades

| De (Entidade)     | Para (Entidade)    | Cardinalidade |
|-------------------|---------------------|----------------|
| Produtor          | Plantacao           | 1 : N          |
| Plantacao         | Leitura_Sensor      | 1 : N          |
| Sensor            | Leitura_Sensor      | 1 : N          |
| Plantacao         | Ajuste_Aplicacao    | 1 : N          |
| Plantacao         | Cultura             | N : N (via Plantacao_Cultura) |

