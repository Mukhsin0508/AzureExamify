# AzureExamify
Experimental

## Django Channels City Overview
```mermaid
flowchart TB
    subgraph MagicalCity["Django Magical City"]
        direction TB
        
        subgraph PostOffice["Traditional Django (WSGI)"]
            HTTP[("HTTP Letters<br/>Request/Response")]
            Views["Regular Views<br/>(Letter Handlers)"]
            HTTP --> Views
        end

        subgraph Highway["ASGI Magic Highway"]
            WS[("WebSocket<br/>Live Calls")]
            Events["Real-time Events<br/>(Messages)"]
            WS --> Events
        end

        subgraph Operator["Channels (Telephone Operator)"]
            Router["Connection Router"]
            WS --> Router
        end

        subgraph Wizards["Consumers (Wizard Spellbooks)"]
            Consumer1["Consumer Instance 1<br/>(Active Conversation)"]
            Consumer2["Consumer Instance 2<br/>(Active Conversation)"]
            Consumer3["Consumer Instance 3<br/>(Active Conversation)"]
        end

        subgraph Tubes["Channel Layers<br/>(Magical Mail Tubes)"]
            Broadcaster["Message Broadcaster"]
        end

        Router --> Consumer1
        Router --> Consumer2
        Router --> Consumer3
        
        Consumer1 --> Broadcaster
        Consumer2 --> Broadcaster
        Consumer3 --> Broadcaster
        
        Broadcaster --> Consumer1
        Broadcaster --> Consumer2
        Broadcaster --> Consumer3
    end

    style MagicalCity fill:#f5f5f5,stroke:#333
    style PostOffice fill:#e1f5fe,stroke:#01579b
    style Highway fill:#f3e5f5,stroke:#4a148c
    style Operator fill:#fff3e0,stroke:#e65100
    style Wizards fill:#e8f5e9,stroke:#1b5e20
    style Tubes fill:#fce4ec,stroke:#880e4f
```

### Speech-to-Speech Real-time Communication with LLM via Django Channels

```mermaid
graph TB
    classDef userClient fill:#ff9999,stroke:#ff0000,stroke-width:2px,color:#000
    classDef audioProcessing fill:#99ff99,stroke:#00ff00,stroke-width:2px,color:#000
    classDef djangoChannels fill:#9999ff,stroke:#0000ff,stroke-width:2px,color:#000
    classDef llmSystem fill:#ffff99,stroke:#ffff00,stroke-width:2px,color:#000
    classDef messageFlow fill:#ff99ff,stroke:#ff00ff,stroke-width:2px,color:#000

    subgraph Client["🎧 User's Browser"]
        Mic["🎤 Microphone Input"]
        Speaker["🔊 Speaker Output"]
        ClientWS["📡 WebSocket Client"]
    end
    
    subgraph AudioSystem["🎵 Audio Processing Tower"]
        STT["🗣️ Speech-to-Text<br/>Whisper API"]
        TTS["📢 Text-to-Speech<br/>ElevenLabs API"]
    end
    
    subgraph DjangoRealm["🏰 Django Magical Realm"]
        direction TB
        subgraph Channels["🌈 Django Channels"]
            Router["🔄 Connection Router"]
            Consumer["✨ Speech Consumer<br/>(Conversation Handler)"]
        end
        
        subgraph MessageHub["📬 Channel Layers"]
            Broadcast["📡 Message Broadcaster"]
            SessionState["📝 Conversation State"]
        end
    end
    
    subgraph LLMWorld["🤖 LLM Dimension"]
        LLMProcess["🧠 Language Model<br/>Claude/GPT"]
        Memory["💭 Conversation Memory"]
    end

    %% Flow of conversation
    Mic -->|"Raw Audio"| ClientWS
    ClientWS -->|"Audio Stream"| Router
    Router -->|"New Connection"| Consumer
    Consumer -->|"Audio Data"| STT
    STT -->|"Transcribed Text"| Consumer
    Consumer -->|"User Message"| LLMProcess
    LLMProcess -->|"Response"| Consumer
    Consumer -->|"Text Response"| TTS
    TTS -->|"Generated Audio"| Consumer
    Consumer -->|"Audio Stream"| ClientWS
    ClientWS -->|"Audio Data"| Speaker
    
    %% State management
    LLMProcess ---|"Update Memory"| Memory
    Consumer ---|"Save State"| SessionState
    
    class Client userClient
    class AudioSystem audioProcessing
    class DjangoRealm djangoChannels
    class LLMWorld llmSystem
    class MessageHub messageFlow
```

### Journey of a "Hello" Through the Django Channels System
```mermaid
sequenceDiagram
    participant U as 👤 User
    participant B as 🌐 Browser
    participant C as 🎭 Channels
    participant SC as ⚡ Consumer
    participant STT as 🎤 STT
    participant LLM as 🤖 LLM
    participant TTS as 🔊 TTS

    Note over U,TTS: When User Says "Hello"
    U->>B: Speaks "Hello"
    B->>C: Sends audio stream
    C->>SC: Routes to consumer
    SC->>STT: Processes audio
    STT->>SC: Returns "hello" text
    SC->>LLM: Sends message + context

    Note over LLM: Processing...
    LLM->>SC: "Hi! How can I help?"
    
    SC->>TTS: Convert to speech
    TTS->>SC: Audio stream
    SC->>C: WebSocket message
    C->>B: Audio delivery
    B->>U: Plays response

    Note over SC,LLM: Conversation state updates in background
```