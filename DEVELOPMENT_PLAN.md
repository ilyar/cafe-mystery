# План развития проекта "Тайна Ночного Кафе"

## Текущее состояние

Проект представляет собой интерактивную 3D игру в браузере с:
- Three.js сцена с кафе
- 3 NPC персонажа с диалогами
- Система отношений и инвентаря
- Ветвящиеся диалоги

## Архитектура проекта

### Файловая структура

```
cafe-mystery/
├── index.html              # Основной файл (всё в одном файле)
├── README.md               # Основная документация
├── DEVELOPMENT_PLAN.md     # Этот файл - план развития
├── assets/                 # Для будущих ресурсов
│   ├── models/             # GLTF модели персонажей
│   ├── textures/           # Текстуры материалов
│   ├── audio/              # Звуковые эффекты
│   └── fonts/              # Локальные шрифты
└── src/                    # Для разделения кода
    ├── game.js             # Игровая логика
    ├── scenes/             # 3D сцены
    ├── characters/         # Персонажи
    ├── dialogue/           # Система диалогов
    ├── ui/                 # UI компоненты
    └── utils/              # Утилиты
```

## Технические детали

### Three.js настройки

```javascript
renderer = {
    antialias: true,
    shadowMap: PCFSoftShadowMap,
    toneMapping: ACESFilmicToneMapping,
    toneMappingExposure: 2.5,
    pixelRatio: min(devicePixelRatio, 2)
}

camera = {
    type: PerspectiveCamera,
    fov: 60,
    position: { x: 0, y: 3, z: 6 }
}
```

### Освещение (текущее)

```
AmbientLight: 0x3a3020, intensity 0.8
HemisphereLight: 0x4a3a25/0x2a1a10, intensity 0.7
SpotLight (chandelier): 0xe8c884, intensity 5.0
PointLight[] (accent): 5 источников, intensity 2.5
PointLight[] (candles): 5 источников, intensity 1.5
PointLight (fill): 0xc8b898, intensity 2.0
```

### Персонажи

Каждый NPC — это `THREE.Group` состоящий из:
- Голова (SphereGeometry)
- Глаза (SphereGeometry x2)
- Зрачки (SphereGeometry x2)
- Волосы (разные варианты)
- Туловище (CylinderGeometry)
- Руки (CylinderGeometry x2)
- Кисти (SphereGeometry x2)
- Ноги (CylinderGeometry x2)

### Система диалогов

```javascript
// Структура узла диалога
{
    text: 'Текст...',
    relation: 10,                    // Изменение отношения
    effect: {                         // Эффекты
        addItem: 'предмет',
        clue: 'улика',
        quest: 'задание',
        unlock: 'локация',
        vision: 'эффект',
        found: 'находка'
    },
    choices: [                        // Варианты выбора
        { text: '...', next: 'node', relation: 5, requires: 'item' }
    ]
}
```

### Игровое состояние

```javascript
gameState = {
    relationships: { elena: 50, marco: 50, nina: 50 },
    inventory: [],
    cluesFound: 0,
    talkedTo: { elena: false, marco: false, nina: false },
    day: 1,
    ending: null
}
```

## План развития по этапам

### Этап 1: Улучшение визуала (Приоритет: Высокий)

#### 1.1 Замена геометрии персонажей
- [ ] Заменить простые цилиндры на детализированные модели
- [ ] Добавить скелетную анимацию (Mixamo)
- [ ] Добавить PBR текстуры для кожи и одежды
- [ ] Добавить детали лица (брови, рот, нос)
- [ ] Добавить разные варианты одежды

#### 1.2 Улучшение освещения
- [ ] Добавить постобработку (bloom через EffectComposer)
- [ ] Добавить SSAO (Screen Space Ambient Occlusion)
- [ ] Добавить глубинную резкость (DOF)
- [ ] Добавить эффекты свечения (emissive materials)
- [ ] Настроить тени (contact shadows, soft shadows)

#### 1.3 Окружение
- [ ] Добавить текстуры для стен и пола
- [ ] Добавить больше декоративных элементов
- [ ] Добавить интерактивные объекты (двери, шкафы)
- [ ] Добавить эффекты (туман, пыль)

### Этап 2: Геймплей (Приоритет: Высокий)

#### 2.1 Перемещение
- [ ] Добавить WASD управление
- [ ] Добавить камеру от третьего лица
- [ ] Добавить коллизии
- [ ] Добавить точки взаимодействия

#### 2.2 Инвентарь
- [ ] Расширить систему инвентаря
- [ ] Добавить использование предметов
- [ ] Добавить комбинации предметов
- [ ] Добавить UI инвентаря

#### 2.3 Сохранение
- [ ] Добавить localStorage для сохранения
- [ ] Добавить систему чекпоинтов
- [ ] Добавить меню сохранения/загрузки

### Этап 3: Расширение контента (Приоритет: Средний)

#### 3.1 Новые NPC
- [ ] Добавить 2-3 новых персонажа
- [ ] Добавить диалоги и квесты
- [ ] Добавить уникальные анимации

#### 3.2 Новые локации
- [ ] Добавить подвал (ключевая локация)
- [ ] Добавить заднюю комнату
- [ ] Добавить улицу перед кафе

#### 3.3 Сюжет
- [ ] Добавить систему квестов
- [ ] Добавить несколько концовок
- [ ] Добавить систему "репутации"
- [ ] Добавить коллекцию Маркуса

### Этап 4: Полировка (Приоритет: Низкий)

#### 4.1 Аудио
- [ ] Добавить фоновую музыку
- [ ] Добавить звуковые эффекты
- [ ] Добавить озвучку диалогов

#### 4.2 UI/UX
- [ ] Добавить анимацию текста (typewriter)
- [ ] Добавить портреты NPC
- [ ] Добавить мини-карту
- [ ] Добавить туториал

#### 4.3 Оптимизация
- [ ] Оптимизировать рендеринг
- [ ] Добавить LOD для объектов
- [ ] Добавить прогрессивную загрузку

## Технические рекомендации

### Для добавления GLTF моделей

```javascript
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';

const loader = new GLTFLoader();
loader.load('assets/models/character.glb', (gltf) => {
    const model = gltf.scene;
    scene.add(model);
    
    // Настроить анимации
    const mixer = new THREE.AnimationMixer(model);
    const clips = gltf.animations;
    // ...
});
```

### Для добавления постобработки

```javascript
import { EffectComposer } from 'three/examples/jsm/postprocessing/EffectComposer.js';
import { RenderPass } from 'three/examples/jsm/postprocessing/RenderPass.js';
import { UnrealBloomPass } from 'three/examples/jsm/postprocessing/UnrealBloomPass.js';

const composer = new EffectComposer(renderer);
composer.addPass(new RenderPass(scene, camera));

const bloomPass = new UnrealBloomPass(
    new THREE.Vector2(window.innerWidth, window.innerHeight),
    1.5,  // strength
    0.4,  // radius
    0.85  // threshold
);
composer.addPass(bloomPass);

// В animate():
composer.render();
```

### Для добавления WASD управления

```javascript
const keys = { w: false, a: false, s: false, d: false };

document.addEventListener('keydown', (e) => {
    keys[e.key.toLowerCase()] = true;
});

document.addEventListener('keyup', (e) => {
    keys[e.key.toLowerCase()] = false;
});

// В animate():
const speed = 0.05;
if (keys.w) camera.position.z -= speed;
if (keys.s) camera.position.z += speed;
if (keys.a) camera.position.x -= speed;
if (keys.d) camera.position.x += speed;
```

### Для добавления сохранения

```javascript
function saveGame() {
    localStorage.setItem('cafeMysterySave', JSON.stringify(gameState));
}

function loadGame() {
    const saved = localStorage.getItem('cafeMysterySave');
    if (saved) {
        Object.assign(gameState, JSON.parse(saved));
    }
}
```

## Часто используемые паттерны

### Добавление нового диалогового узла

```javascript
// В npcData[персонаж].dialogueTree:
newNode: {
    text: 'Новый текст диалога',
    relation: 15,
    effect: { addItem: 'новый предмет' },
    choices: [
        { text: 'Вариант 1', next: 'anotherNode', relation: 10 },
        { text: 'Вариант 2', next: 'endNode', requires: 'нужный предмет' }
    ]
}
```

### Добавление нового предмета

```javascript
// 1. Добавить в эффект диалога
effect: { addItem: 'название предмета' }

// 2. Добавить иконку (опционально)
const icons = {
    'название предмета': '🔧',
    // ...
};

// 3. Добавить проверку в choice
{ text: 'Использовать предмет', next: 'result', requires: 'название предмета' }
```

### Добавление новой анимации

```javascript
// В animate():
npcs.forEach(npc => {
    // Новая анимация
    const head = npc.children[0];
    if (head && npc.userData.talking) {
        head.rotation.y = Math.sin(time * 3) * 0.2;  // Кивание
    }
});
```

## Чек-лист перед коммитом

- [ ] Код работает без ошибок в консоли
- [ ] Все диалоги проверены
- [ ] Инвентарь работает корректно
- [ ] Отношения обновляются правильно
- [ ] Анимации плавные
- [ ] Освещение адекватное
- [ ] Тест на разных браузерах (Chrome, Firefox)
- [ ] README обновлён

## Полезные ссылки

- Three.js Docs: https://threejs.org/docs/
- Three.js Examples: https://threejs.org/examples/
- Mixamo (анимации): https://www.mixamo.com/
- Poly Haven (текстуры): https://polyhaven.com/
- Sketchfab (модели): https://sketchfab.com/

## Контакты

Проект разработан для образовательных целей. Для вопросов по развитию — обращайтесь к документации.

---

*Этот документ должен обновляться при каждом значительном изменении проекта.*
