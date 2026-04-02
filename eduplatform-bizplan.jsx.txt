import { useState } from "react";

const sections = [
  { id: "overview", label: "О продукте" },
  { id: "problem", label: "Проблема & Решение" },
  { id: "bottleneck", label: "Узкое горлышко" },
  { id: "features", label: "Функционал" },
  { id: "university", label: "ВУЗ-калькулятор" },
  { id: "monetization", label: "Монетизация" },
  { id: "competitors", label: "Конкуренты" },
  { id: "seo", label: "SEO-стратегия" },
  { id: "ideas", label: "Мощные идеи" },
  { id: "roadmap", label: "Роадмап" },
];

const accent = "#FF5733";
const accent2 = "#FFB800";
const dark = "#0A0A0F";
const card = "#13131A";
const border = "#2A2A3A";
const muted = "#6B6B80";

export default function BizPlan() {
  const [active, setActive] = useState("overview");

  return (
    <div style={{
      fontFamily: "'Georgia', serif",
      background: dark,
      color: "#E8E8F0",
      minHeight: "100vh",
      display: "flex",
      flexDirection: "column",
    }}>
      {/* Hero */}
      <div style={{
        background: `linear-gradient(135deg, #0A0A0F 0%, #12001A 50%, #0A0A0F 100%)`,
        borderBottom: `1px solid ${border}`,
        padding: "48px 32px 40px",
        position: "relative",
        overflow: "hidden",
      }}>
        <div style={{
          position: "absolute", top: 0, left: 0, right: 0, bottom: 0,
          backgroundImage: `radial-gradient(ellipse at 20% 50%, rgba(255,87,51,0.08) 0%, transparent 60%), radial-gradient(ellipse at 80% 20%, rgba(255,184,0,0.06) 0%, transparent 50%)`,
          pointerEvents: "none",
        }} />
        <div style={{ maxWidth: 960, margin: "0 auto", position: "relative" }}>
          <div style={{
            display: "inline-block",
            background: "rgba(255,87,51,0.12)",
            border: `1px solid rgba(255,87,51,0.3)`,
            borderRadius: 4,
            padding: "4px 12px",
            fontSize: 11,
            letterSpacing: "0.15em",
            textTransform: "uppercase",
            color: accent,
            marginBottom: 20,
            fontFamily: "monospace",
          }}>Бизнес-план · v1.0 · Конфиденциально</div>
          <h1 style={{
            fontSize: "clamp(32px, 5vw, 56px)",
            fontWeight: 700,
            margin: "0 0 12px",
            lineHeight: 1.1,
            letterSpacing: "-0.02em",
          }}>
            <span style={{ color: "#fff" }}>EXAM</span>
            <span style={{ color: accent }}>PATH</span>
          </h1>
          <p style={{ fontSize: 18, color: "#A0A0B8", maxWidth: 600, margin: "0 0 28px", lineHeight: 1.6 }}>
            Образовательная экосистема нового поколения — подготовка к ОГЭ/ЕГЭ, менторство, курсы по профессиям и умный ВУЗ-навигатор в одном приложении.
          </p>
          <div style={{ display: "flex", gap: 24, flexWrap: "wrap" }}>
            {[
              ["🎯", "Школьники 8–11 кл."],
              ["👨‍🏫", "Репетиторы & менторы"],
              ["🏛️", "Абитуриенты"],
              ["💼", "Профессиональные курсы"],
            ].map(([icon, label]) => (
              <div key={label} style={{ display: "flex", alignItems: "center", gap: 8, fontSize: 14, color: "#9090A8" }}>
                <span style={{ fontSize: 18 }}>{icon}</span>
                {label}
              </div>
            ))}
          </div>
        </div>
      </div>

      {/* Nav */}
      <div style={{
        borderBottom: `1px solid ${border}`,
        overflowX: "auto",
        background: "#0D0D14",
        position: "sticky", top: 0, zIndex: 100,
      }}>
        <div style={{ display: "flex", maxWidth: 960, margin: "0 auto", padding: "0 24px" }}>
          {sections.map(s => (
            <button
              key={s.id}
              onClick={() => setActive(s.id)}
              style={{
                background: "none", border: "none", cursor: "pointer",
                padding: "14px 16px",
                fontSize: 13,
                color: active === s.id ? accent : muted,
                borderBottom: active === s.id ? `2px solid ${accent}` : "2px solid transparent",
                whiteSpace: "nowrap",
                fontFamily: "inherit",
                transition: "color 0.2s",
              }}
            >{s.label}</button>
          ))}
        </div>
      </div>

      {/* Content */}
      <div style={{ maxWidth: 960, margin: "0 auto", padding: "40px 24px", width: "100%", boxSizing: "border-box" }}>
        {active === "overview" && <Overview />}
        {active === "problem" && <Problem />}
        {active === "bottleneck" && <Bottleneck />}
        {active === "features" && <Features />}
        {active === "university" && <University />}
        {active === "monetization" && <Monetization />}
        {active === "competitors" && <Competitors />}
        {active === "seo" && <SEO />}
        {active === "ideas" && <Ideas />}
        {active === "roadmap" && <Roadmap />}
      </div>
    </div>
  );
}

/* ─── Shared components ─── */
function SectionTitle({ children, sub }) {
  return (
    <div style={{ marginBottom: 32 }}>
      <h2 style={{ fontSize: 28, fontWeight: 700, margin: "0 0 8px", color: "#fff", letterSpacing: "-0.01em" }}>{children}</h2>
      {sub && <p style={{ color: muted, fontSize: 15, margin: 0, lineHeight: 1.6 }}>{sub}</p>}
    </div>
  );
}

function Card({ children, highlight }) {
  return (
    <div style={{
      background: card,
      border: `1px solid ${highlight ? "rgba(255,87,51,0.35)" : border}`,
      borderRadius: 10,
      padding: "24px",
      marginBottom: 16,
      boxShadow: highlight ? "0 0 24px rgba(255,87,51,0.06)" : "none",
    }}>{children}</div>
  );
}

function Tag({ children, color }) {
  return (
    <span style={{
      display: "inline-block",
      background: `${color || accent}18`,
      border: `1px solid ${color || accent}40`,
      color: color || accent,
      borderRadius: 4,
      padding: "2px 10px",
      fontSize: 12,
      letterSpacing: "0.05em",
      marginRight: 8,
      marginBottom: 6,
    }}>{children}</span>
  );
}

function Grid({ children, cols = 2 }) {
  return (
    <div style={{
      display: "grid",
      gridTemplateColumns: `repeat(${cols}, 1fr)`,
      gap: 16,
    }}>{children}</div>
  );
}

/* ─── Section: Overview ─── */
function Overview() {
  return (
    <div>
      <SectionTitle sub="Что такое ExamPath и зачем это нужно рынку">О продукте</SectionTitle>
      <Card highlight>
        <p style={{ fontSize: 16, lineHeight: 1.8, color: "#CCC", margin: 0 }}>
          <strong style={{ color: "#fff" }}>ExamPath</strong> — это единая образовательная платформа (сайт + мобильное приложение iOS/Android), которая объединяет:
          подготовку к ОГЭ и ЕГЭ по всем предметам, авторские курсы профессиональных менторов по дизайну, разработке и другим специальностям,
          маркетплейс репетиторов, тренировочные тесты в формате реальных экзаменов и умный ВУЗ-навигатор с калькулятором проходных баллов.
        </p>
      </Card>
      <Grid cols={3}>
        {[
          { n: "14M+", l: "школьников в России" },
          { n: "800K+", l: "сдают ЕГЭ ежегодно" },
          { n: "₽280B", l: "рынок EdTech RU 2025" },
        ].map(({ n, l }) => (
          <Card key={n}>
            <div style={{ fontSize: 36, fontWeight: 700, color: accent, marginBottom: 6 }}>{n}</div>
            <div style={{ color: muted, fontSize: 14 }}>{l}</div>
          </Card>
        ))}
      </Grid>
      <Card>
        <h3 style={{ color: "#fff", marginTop: 0, fontSize: 16 }}>Целевые аудитории</h3>
        <div>
          {[
            ["Школьники 8–11 класс", "Основная ЦА — сдают ОГЭ/ЕГЭ, ищут структурированную подготовку и тренировочные тесты"],
            ["Абитуриенты", "Выбирают ВУЗ, хотят знать проходные баллы, фильтровать специальности и сразу подать документы"],
            ["Репетиторы", "Хотят монетизировать свои знания, получать учеников без посредников"],
            ["Менторы-профессионалы", "Дизайнеры, разработчики, маркетологи — создают курсы и продают на платформе"],
            ["Родители", "Оплачивают подписку, хотят видеть прогресс ребёнка и результаты"],
          ].map(([title, desc]) => (
            <div key={title} style={{ display: "flex", gap: 16, padding: "12px 0", borderBottom: `1px solid ${border}` }}>
              <div style={{ width: 8, height: 8, borderRadius: "50%", background: accent, marginTop: 6, flexShrink: 0 }} />
              <div>
                <div style={{ color: "#fff", fontWeight: 600, fontSize: 14, marginBottom: 2 }}>{title}</div>
                <div style={{ color: muted, fontSize: 13 }}>{desc}</div>
              </div>
            </div>
          ))}
        </div>
      </Card>
    </div>
  );
}

/* ─── Section: Problem ─── */
function Problem() {
  return (
    <div>
      <SectionTitle sub="Какую проблему решает ExamPath среди конкурентов">Проблема & Решение</SectionTitle>
      <Card>
        <h3 style={{ color: accent, marginTop: 0 }}>⚠️ Боли рынка сегодня</h3>
        {[
          ["Фрагментация", "Школьник использует 4–6 разных сервисов: Решу ЕГЭ для тестов, Skysmart для уроков, Репетитор.ру для поиска учителя, ВУЗопедию для выбора ВУЗа. Единого пространства нет."],
          ["Нет пути от знаний к профессии", "После сдачи ЕГЭ ребёнок теряется: куда идти учиться? Как выбрать специальность? Платформы заканчиваются на экзамене."],
          ["Репетиторы работают в Instagram/VK", "Нет удобного инструмента для ведения учеников, расписания, оплаты, материалов — всё в мессенджерах."],
          ["Профессиональные курсы отдельно", "Stepik, Skillbox — для взрослых. Школьникам с карьерными амбициями некуда идти, пока они ещё в школе."],
          ["Нет умного подбора ВУЗа", "Существующие агрегаторы не привязаны к баллам ЕГЭ пользователя и не показывают шансы поступления в реальном времени."],
        ].map(([title, desc]) => (
          <div key={title} style={{ padding: "12px 0", borderBottom: `1px solid ${border}` }}>
            <div style={{ color: "#fff", fontWeight: 600, marginBottom: 4, fontSize: 15 }}>🔴 {title}</div>
            <div style={{ color: muted, fontSize: 14, lineHeight: 1.6 }}>{desc}</div>
          </div>
        ))}
      </Card>
      <Card highlight>
        <h3 style={{ color: "#4CAF50", marginTop: 0 }}>✅ Что решает ExamPath</h3>
        <p style={{ color: "#CCC", lineHeight: 1.7, fontSize: 15, margin: "0 0 16px" }}>
          Одна платформа закрывает весь путь ученика: <strong style={{ color: "#fff" }}>8 класс → ОГЭ → 11 класс → ЕГЭ → выбор ВУЗа → поступление → профессиональные навыки</strong>.
          Это не просто сайт с тестами — это карьерный трек, начинающийся в школе.
        </p>
        <div style={{ display: "flex", gap: 8, flexWrap: "wrap" }}>
          {["Всё в одном приложении", "Персонализация AI", "Монетизация для репетиторов", "Живые данные ВУЗов", "Курсы от практиков"].map(t => (
            <Tag key={t} color="#4CAF50">{t}</Tag>
          ))}
        </div>
      </Card>
    </div>
  );
}

/* ─── Section: Bottleneck ─── */
function Bottleneck() {
  return (
    <div>
      <SectionTitle sub="Главные риски и как их решить на старте">Узкое горлышко</SectionTitle>
      {[
        {
          problem: "Проблема курицы и яйца",
          severity: "КРИТИЧНО",
          color: "#FF4444",
          desc: "Без учеников репетиторы не придут. Без репетиторов ученики не придут. Классическая ловушка маркетплейса.",
          solution: [
            "Запустить платформу сначала как B2C-продукт (тесты + курсы от команды) — без репетиторов",
            "Накопить базу школьников через SEO и виральный контент (TikTok/Reels)",
            "Только после 10 000 MAU открыть маркетплейс репетиторов с готовой аудиторией",
          ],
        },
        {
          problem: "Качество контента",
          severity: "ВЫСОКИЙ",
          color: "#FF8C00",
          desc: "Тесты должны совпадать с реальным форматом ФИПИ. Любое несоответствие убивает доверие. Репетиторы могут выставлять некачественные материалы.",
          solution: [
            "Нанять методистов с опытом в ФИПИ или Яндекс.ЕГЭ для верификации тестов",
            "Ввести систему рейтинга и модерации контента репетиторов (минимальный рейтинг для публикации)",
            "Автоматическая проверка структуры тестовых заданий перед публикацией",
          ],
        },
        {
          problem: "Устаревание данных ВУЗов",
          severity: "СРЕДНИЙ",
          color: "#FFB800",
          desc: "Проходные баллы и количество бюджетных мест меняются каждый год. Неактуальные данные = юридические риски и потеря доверия.",
          solution: [
            "Прямая интеграция с API Госуслуг и официальными сайтами приёмных комиссий",
            "Парсинг с автоматическим обновлением перед сезоном поступления (май–август)",
            "Партнёрство с ВУЗами: они сами загружают данные за верифицированный бейдж",
          ],
        },
        {
          problem: "Отток после ЕГЭ",
          severity: "СРЕДНИЙ",
          color: "#FFB800",
          desc: "После сдачи экзамена пользователь уходит. Платформа без удержания = дырявое ведро.",
          solution: [
            "Продолжение пути: курсы по профессиям держат пользователя после ЕГЭ",
            "Геймификация и стрики (Duolingo-механика) создают привычку",
            "Менторство и карьерные треки — долгосрочное удержание на 1–2 года",
          ],
        },
      ].map(({ problem, severity, color, desc, solution }) => (
        <Card key={problem}>
          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", marginBottom: 10 }}>
            <h3 style={{ color: "#fff", margin: 0, fontSize: 16 }}>🔧 {problem}</h3>
            <Tag color={color}>{severity}</Tag>
          </div>
          <p style={{ color: muted, fontSize: 14, lineHeight: 1.6, margin: "0 0 14px" }}>{desc}</p>
          <div style={{ background: "#0A0A0F", borderRadius: 6, padding: "12px 16px" }}>
            <div style={{ color: "#4CAF50", fontSize: 12, letterSpacing: "0.1em", marginBottom: 8 }}>РЕШЕНИЕ</div>
            {solution.map((s, i) => (
              <div key={i} style={{ display: "flex", gap: 10, marginBottom: 6, fontSize: 13, color: "#CCC" }}>
                <span style={{ color: "#4CAF50", flexShrink: 0 }}>→</span>{s}
              </div>
            ))}
          </div>
        </Card>
      ))}
    </div>
  );
}

/* ─── Section: Features ─── */
function Features() {
  return (
    <div>
      <SectionTitle sub="Полный функционал платформы по модулям">Функционал</SectionTitle>
      <Grid cols={2}>
        {[
          {
            icon: "📝", title: "Тренировочные тесты ОГЭ/ЕГЭ",
            items: [
              "Все предметы, все варианты",
              "Формат = реальный экзамен ФИПИ",
              "Разбор ошибок с объяснением",
              "Статистика по темам/заданиям",
              "Таймер, черновик, ввод с клавиатуры",
            ]
          },
          {
            icon: "📚", title: "Авторские курсы & методики",
            items: [
              "Видеоуроки по темам ЕГЭ",
              "Структурированная теория",
              "Интерактивные задания внутри",
              "Прогресс-бар и сертификаты",
              "Офлайн-режим (приложение)",
            ]
          },
          {
            icon: "👨‍🏫", title: "Маркетплейс репетиторов",
            items: [
              "Профиль + портфолио + отзывы",
              "Встроенный видеозвонок",
              "Расписание и бронирование",
              "Безопасная оплата (эскроу)",
              "Чат с учеником",
            ]
          },
          {
            icon: "🎓", title: "Профессиональные курсы",
            items: [
              "Дизайн, веб-разработка, SMM",
              "Курсы от практикующих менторов",
              "Проектная работа + ревью",
              "Карьерный трек и портфолио",
              "Доступ для старшеклассников",
            ]
          },
          {
            icon: "🤝", title: "Менторство",
            items: [
              "1-на-1 сессии с экспертами",
              "Групповые воркшопы",
              "Карьерные консультации",
              "Ревью резюме и портфолио",
              "Нетворкинг с профи",
            ]
          },
          {
            icon: "🤖", title: "AI-ассистент",
            items: [
              "Персональный план подготовки",
              "Объяснение сложных тем",
              "Предиктивный анализ баллов",
              "Рекомендации курсов по слабым темам",
              "Чат-помощник 24/7",
            ]
          },
        ].map(({ icon, title, items }) => (
          <Card key={title}>
            <div style={{ fontSize: 28, marginBottom: 10 }}>{icon}</div>
            <h3 style={{ color: "#fff", marginTop: 0, fontSize: 15, marginBottom: 12 }}>{title}</h3>
            {items.map(item => (
              <div key={item} style={{ fontSize: 13, color: muted, marginBottom: 5, display: "flex", gap: 8 }}>
                <span style={{ color: accent }}>·</span>{item}
              </div>
            ))}
          </Card>
        ))}
      </Grid>
    </div>
  );
}

/* ─── Section: University ─── */
function University() {
  return (
    <div>
      <SectionTitle sub="Умный навигатор для выбора ВУЗа — уникальная фича платформы">ВУЗ-калькулятор</SectionTitle>
      <Card highlight>
        <h3 style={{ color: accent, marginTop: 0 }}>🏛️ Как это работает</h3>
        <p style={{ color: "#CCC", lineHeight: 1.7, fontSize: 15 }}>
          Пользователь вводит свои баллы по предметам ЕГЭ (или они берутся из прогресса на платформе), 
          выбирает желаемый регион и направление — система показывает список ВУЗов, 
          куда он <strong style={{ color: "#4CAF50" }}>проходит</strong>, где <strong style={{ color: accent2 }}>в зоне риска</strong>, 
          и куда <strong style={{ color: "#FF4444" }}>не пройдёт</strong>.
        </p>
      </Card>
      <Grid cols={2}>
        {[
          {
            title: "Фильтры",
            items: ["По предметам ЕГЭ", "По специальности/направлению", "По региону и городу", "Бюджет / контракт", "Общежитие да/нет", "Рейтинг ВУЗа (QS, Форбс)", "Военная кафедра"]
          },
          {
            title: "Что показывает",
            items: ["Проходной балл прошлого года", "Количество бюджетных мест", "Стоимость контракта", "Шанс поступления в %", "Средний балл поступивших", "Прямая ссылка на сайт ВУЗа", "Контакты приёмной комиссии"]
          },
        ].map(({ title, items }) => (
          <Card key={title}>
            <h3 style={{ color: "#fff", marginTop: 0, fontSize: 15 }}>{title}</h3>
            {items.map(i => (
              <div key={i} style={{ fontSize: 13, color: muted, marginBottom: 6, display: "flex", gap: 8 }}>
                <span style={{ color: accent2 }}>✓</span>{i}
              </div>
            ))}
          </Card>
        ))}
      </Grid>
      <Card>
        <h3 style={{ color: "#fff", marginTop: 0 }}>🔗 Прямой доступ к ВУЗам</h3>
        <p style={{ color: muted, fontSize: 14, lineHeight: 1.6 }}>
          Каждый ВУЗ имеет верифицированную карточку с актуальным номером телефона приёмной комиссии, 
          email, ссылкой на сайт подачи документов (включая Госуслуги) и датами подачи заявлений. 
          Данные обновляются ежегодно, ВУЗы могут верифицировать свои данные самостоятельно через партнёрский кабинет.
        </p>
        <div style={{ display: "flex", gap: 8, flexWrap: "wrap", marginTop: 12 }}>
          {["Актуальные телефоны", "Прямые ссылки на подачу", "Даты кампании", "Карта на кампус", "Виртуальный тур"].map(t => (
            <Tag key={t} color={accent2}>{t}</Tag>
          ))}
        </div>
      </Card>
    </div>
  );
}

/* ─── Section: Monetization ─── */
function Monetization() {
  return (
    <div>
      <SectionTitle sub="Несколько потоков дохода — устойчивая модель">Монетизация</SectionTitle>
      <Grid cols={2}>
        {[
          { title: "Подписка B2C", icon: "💳", color: accent, items: ["Базовый FREE: тесты, ограниченные курсы", "Premium ₽590/мес: всё без ограничений + AI-план", "Family ₽990/мес: до 3 детей", "Годовой план со скидкой 30%"] },
          { title: "Комиссия маркетплейса", icon: "🤝", color: "#4CAF50", items: ["20% с каждой сделки репетитора", "15% с продажи курсов менторов", "Продвинутый профиль: ₽1490/мес", "Выделенное место в поиске"] },
          { title: "B2B (Школы)", icon: "🏫", color: accent2, items: ["Лицензия на школу от ₽15 000/год", "Кабинет учителя + статистика класса", "Корпоративная подготовка к ЕГЭ", "Белый лейбл для школ"] },
          { title: "Реклама & Партнёрства", icon: "📣", color: "#9B59B6", items: ["Нативная реклама курсов в каталоге", "Партнёрство с ВУЗами (верифицированный профиль)", "Онлайн-олимпиады от брендов", "Реферальная программа"] },
        ].map(({ title, icon, color, items }) => (
          <Card key={title}>
            <div style={{ display: "flex", gap: 12, alignItems: "center", marginBottom: 12 }}>
              <span style={{ fontSize: 24 }}>{icon}</span>
              <h3 style={{ color: color, margin: 0, fontSize: 15 }}>{title}</h3>
            </div>
            {items.map(i => (
              <div key={i} style={{ fontSize: 13, color: muted, marginBottom: 6, display: "flex", gap: 8 }}>
                <span style={{ color }}>→</span>{i}
              </div>
            ))}
          </Card>
        ))}
      </Grid>
      <Card highlight>
        <div style={{ display: "flex", gap: 32, flexWrap: "wrap" }}>
          {[
            { label: "Прогноз MAU год 1", value: "50 000" },
            { label: "Конверсия в Premium", value: "8–12%" },
            { label: "ARPU Premium", value: "₽620/мес" },
            { label: "ARR цель год 1", value: "₽37M" },
          ].map(({ label, value }) => (
            <div key={label}>
              <div style={{ fontSize: 26, fontWeight: 700, color: accent }}>{value}</div>
              <div style={{ color: muted, fontSize: 13 }}>{label}</div>
            </div>
          ))}
        </div>
      </Card>
    </div>
  );
}

/* ─── Section: Competitors ─── */
function Competitors() {
  const comps = [
    { name: "Решу ЕГЭ", plus: "Огромная база тестов, SEO-трафик", minus: "Только тесты, нет курсов, репетиторов, ВУЗов. UI устаревший." },
    { name: "Яндекс.Репетитор", plus: "Доверие бренда Яндекс", minus: "Нет тестов ФИПИ-формата, нет ВУЗ-навигатора, нет профкурсов." },
    { name: "Skysmart", plus: "Хорошие интерактивные уроки", minus: "Дорого, нет маркетплейса репетиторов, нет ЕГЭ-тестов в полном формате." },
    { name: "Stepik / Skillbox", plus: "Профкурсы на высоком уровне", minus: "Нет школьной подготовки, нет ОГЭ/ЕГЭ, нет ВУЗ-калькулятора." },
    { name: "Поступи.онлайн", plus: "ВУЗ-навигатор", minus: "Нет образования, нет курсов, нет репетиторов — только навигатор." },
  ];
  return (
    <div>
      <SectionTitle sub="Позиционирование ExamPath среди конкурентов">Конкуренты</SectionTitle>
      <Card highlight>
        <p style={{ color: "#CCC", fontSize: 15, lineHeight: 1.7, margin: 0 }}>
          <strong style={{ color: "#fff" }}>Главное конкурентное преимущество:</strong> ни один игрок не закрывает весь путь школьника. 
          Конкуренты — точечные инструменты. ExamPath — экосистема. Переключение между 5 приложениями vs одно приложение на 4 года.
        </p>
      </Card>
      {comps.map(({ name, plus, minus }) => (
        <Card key={name}>
          <div style={{ display: "flex", gap: 16, alignItems: "flex-start", flexWrap: "wrap" }}>
            <div style={{ minWidth: 140 }}>
              <div style={{ color: "#fff", fontWeight: 700, fontSize: 15 }}>{name}</div>
            </div>
            <div style={{ flex: 1 }}>
              <div style={{ fontSize: 13, color: "#4CAF50", marginBottom: 4 }}>✅ {plus}</div>
              <div style={{ fontSize: 13, color: "#FF6B6B" }}>❌ {minus}</div>
            </div>
          </div>
        </Card>
      ))}
      <Card>
        <h3 style={{ color: "#fff", marginTop: 0 }}>ExamPath vs все: матрица функций</h3>
        <div style={{ overflowX: "auto" }}>
          <table style={{ width: "100%", borderCollapse: "collapse", fontSize: 13 }}>
            <thead>
              <tr>
                {["Функция", "ExamPath", "Решу ЕГЭ", "Яндекс.Реп", "Stepik"].map(h => (
                  <th key={h} style={{ textAlign: "left", padding: "8px 12px", color: h === "ExamPath" ? accent : muted, borderBottom: `1px solid ${border}` }}>{h}</th>
                ))}
              </tr>
            </thead>
            <tbody>
              {[
                ["Тесты ОГЭ/ЕГЭ", "✅", "✅", "⚠️", "❌"],
                ["Авторские курсы", "✅", "❌", "❌", "✅"],
                ["Маркетплейс репет.", "✅", "❌", "✅", "❌"],
                ["Профкурсы", "✅", "❌", "❌", "✅"],
                ["ВУЗ-калькулятор", "✅", "❌", "❌", "❌"],
                ["AI-ассистент", "✅", "❌", "❌", "❌"],
                ["Мобильное приложение", "✅", "⚠️", "✅", "✅"],
              ].map(([feat, ...vals]) => (
                <tr key={feat}>
                  <td style={{ padding: "8px 12px", color: "#CCC", borderBottom: `1px solid ${border}` }}>{feat}</td>
                  {vals.map((v, i) => (
                    <td key={i} style={{ padding: "8px 12px", textAlign: "center", borderBottom: `1px solid ${border}` }}>{v}</td>
                  ))}
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      </Card>
    </div>
  );
}

/* ─── Section: SEO ─── */
function SEO() {
  return (
    <div>
      <SectionTitle sub="Органический рост через поисковой трафик — главный канал">SEO-стратегия</SectionTitle>
      <Card highlight>
        <p style={{ color: "#CCC", lineHeight: 1.7, fontSize: 15, margin: 0 }}>
          SEO — это основа роста ExamPath. Каждый тест, каждая тема ЕГЭ, каждый ВУЗ = SEO-страница. 
          При правильной реализации это <strong style={{ color: accent }}>1M+ органических визитов/мес</strong> без платного трафика.
        </p>
      </Card>
      <Grid cols={2}>
        <Card>
          <h3 style={{ color: accent, marginTop: 0, fontSize: 15 }}>🔑 Семантическое ядро</h3>
          {[
            "решу егэ математика 2025 — 50K/мес",
            "подготовка к огэ русский язык — 35K/мес",
            "тесты егэ биология онлайн — 28K/мес",
            "репетитор по физике онлайн — 22K/мес",
            "проходной балл МГТУ 2025 — 18K/мес",
            "курсы веб-разработки для школьников — 12K/мес",
            "калькулятор баллов егэ — 40K/мес",
          ].map(kw => (
            <div key={kw} style={{ fontSize: 12, color: muted, marginBottom: 6, fontFamily: "monospace", padding: "4px 8px", background: "#0A0A0F", borderRadius: 4 }}>{kw}</div>
          ))}
        </Card>
        <Card>
          <h3 style={{ color: accent2, marginTop: 0, fontSize: 15 }}>📄 Типы SEO-страниц</h3>
          {[
            ["Тест по [предмет] ЕГЭ вариант [N]", "×200 страниц"],
            ["Подготовка к ЕГЭ по [предмет]", "×14 страниц"],
            ["Репетитор по [предмет] онлайн", "×14 страниц"],
            ["[ВУЗ]: проходной балл 2025", "×500+ страниц"],
            ["[Специальность] куда поступить", "×300+ страниц"],
            ["Задание [N] ЕГЭ [предмет] разбор", "×1000+ страниц"],
          ].map(([type, count]) => (
            <div key={type} style={{ display: "flex", justifyContent: "space-between", fontSize: 13, padding: "6px 0", borderBottom: `1px solid ${border}`, color: muted }}>
              <span>{type}</span>
              <Tag color={accent2}>{count}</Tag>
            </div>
          ))}
        </Card>
      </Grid>
      <Card>
        <h3 style={{ color: "#fff", marginTop: 0 }}>🔧 Технический SEO-чеклист</h3>
        <Grid cols={2}>
          {[
            "SSR/Next.js — индексируемые страницы",
            "Structured Data (FAQ, Course, Review)",
            "Breadcrumbs на всех страницах",
            "Скорость <2s LCP (Core Web Vitals)",
            "Sitemap XML с приоритетами",
            "Canonical URL для тестов-дублей",
            "Микроразметка для ВУЗов и курсов",
            "Мобильная адаптация (Mobile-First Index)",
            "Внутренняя перелинковка предметов",
            "Программное создание SEO-страниц",
          ].map(item => (
            <div key={item} style={{ fontSize: 13, color: muted, display: "flex", gap: 8, marginBottom: 8 }}>
              <span style={{ color: "#4CAF50" }}>✓</span>{item}
            </div>
          ))}
        </Grid>
      </Card>
      <Card>
        <h3 style={{ color: "#fff", marginTop: 0 }}>📱 Виральный контент (SMM + SEO)</h3>
        <p style={{ color: muted, fontSize: 14, lineHeight: 1.7 }}>
          TikTok/Reels с разборами заданий ЕГЭ — один из самых эффективных каналов. Каждое видео = ссылка на платформу. 
          Telegram-каналы по предметам с ежедневными задачами. YouTube с полными разборами вариантов — долгосрочное SEO-видео.
        </p>
        <div style={{ display: "flex", gap: 8, flexWrap: "wrap", marginTop: 8 }}>
          {["TikTok разборы заданий", "Telegram Daily ЕГЭ", "YouTube полные варианты", "Instagram Stories-тесты", "VK-сообщества по предметам"].map(t => (
            <Tag key={t}>{t}</Tag>
          ))}
        </div>
      </Card>
    </div>
  );
}

/* ─── Section: Ideas ─── */
function Ideas() {
  return (
    <div>
      <SectionTitle sub="Идеи, которые сделают ExamPath незабываемым продуктом">Мощные идеи</SectionTitle>
      {[
        {
          title: "🧠 AI-персонализация «Мой ЕГЭ-план»",
          desc: "На основе результатов диагностического теста AI строит персональный план подготовки по неделям. «Тебе нужно 3 балла до 80, до ЕГЭ 120 дней, вот точный план». Ни один конкурент этого не делает.",
          tag: "WOW-фича"
        },
        {
          title: "🔮 «Куда я поступлю прямо сейчас»",
          desc: "Динамический калькулятор: пользователь проходит 20-минутный тест по предметам — система прогнозирует текущий балл ЕГЭ и показывает ВУЗы, куда он проходит уже сейчас и куда пройдёт если будет заниматься 2 месяца.",
          tag: "Конверсионная фича"
        },
        {
          title: "🏆 ExamPath Leaderboard & Лиги",
          desc: "Соревнования между школами, классами, городами. Топ-100 по предметам. Школы могут зарегистрировать классы и отслеживать прогресс всего класса. Геймификация = виральность = рост без затрат.",
          tag: "Виральность"
        },
        {
          title: "📱 Offline-режим для приложения",
          desc: "Скачал вариант теста — решаешь в поезде без интернета. Критично для регионов. Конкуренты в браузере — мы в нативном приложении с офлайн-доступом к скачанным курсам.",
          tag: "Региональный охват"
        },
        {
          title: "🎙️ Live-сессии «Разбор варианта вживую»",
          desc: "Репетиторы проводят прямые эфиры с разбором вариантов ЕГЭ. Зрители платят за VIP-доступ с возможностью задать вопрос. YouTube-формат внутри платформы. Записи продаются как курсы.",
          tag: "Новый формат"
        },
        {
          title: "🤝 B2B для школ: «Кабинет учителя»",
          desc: "Учитель создаёт класс, задаёт домашние тесты из базы ExamPath, видит прогресс каждого ученика. Школа покупает лицензию оптом. Это B2B-поток с высоким LTV и низким churn.",
          tag: "B2B"
        },
        {
          title: "🌍 Сообщество выпускников-менторов",
          desc: "Студент МГТУ, поступивший в 2023, становится ментором для абитуриентов 2025. Личный опыт поступления бесценен. Платформа соединяет их. Старшеклассник платит за сессию со студентом топ-ВУЗа.",
          tag: "Community"
        },
        {
          title: "📊 «Дашборд для родителей»",
          desc: "Родитель видит: сколько минут занимался ребёнок, какой прогноз балла ЕГЭ, какие темы западают. Push-уведомления родителю, если ребёнок не занимался 3 дня. Родитель — ЛПР по покупке Premium.",
          tag: "Конверсия"
        },
      ].map(({ title, desc, tag }) => (
        <Card key={title}>
          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", marginBottom: 8 }}>
            <h3 style={{ color: "#fff", margin: 0, fontSize: 15, flex: 1, paddingRight: 12 }}>{title}</h3>
            <Tag>{tag}</Tag>
          </div>
          <p style={{ color: muted, fontSize: 14, lineHeight: 1.6, margin: 0 }}>{desc}</p>
        </Card>
      ))}
    </div>
  );
}

/* ─── Section: Roadmap ─── */
function Roadmap() {
  const phases = [
    {
      phase: "Фаза 1", time: "0–3 месяца", title: "MVP запуск",
      color: accent,
      tasks: [
        "Тесты ОГЭ/ЕГЭ по 5 предметам (математика, русский, физика, химия, история)",
        "Базовые курсы от 3–5 авторских методистов",
        "Сайт + простое мобильное приложение (React Native)",
        "SEO-структура и первые 200 страниц",
        "Telegram-канал и TikTok-стратегия",
      ]
    },
    {
      phase: "Фаза 2", time: "3–6 месяцев", title: "Рост & Маркетплейс",
      color: accent2,
      tasks: [
        "Маркетплейс репетиторов (50+ верифицированных)",
        "Все предметы ЕГЭ/ОГЭ",
        "ВУЗ-калькулятор (топ-200 ВУЗов)",
        "Premium-подписка и платёжная система",
        "B2B пилот с 5–10 школами",
      ]
    },
    {
      phase: "Фаза 3", time: "6–12 месяцев", title: "Экосистема",
      color: "#4CAF50",
      tasks: [
        "AI-персонализация и прогноз баллов",
        "Профессиональные курсы (дизайн, разработка)",
        "Live-сессии и групповые воркшопы",
        "Дашборд для родителей",
        "Gamification & Leaderboard",
      ]
    },
    {
      phase: "Фаза 4", time: "12–24 месяца", title: "Масштабирование",
      color: "#9B59B6",
      tasks: [
        "Партнёрства с топ-ВУЗами",
        "Белый лейбл для школьных сетей",
        "Международная экспансия (СНГ)",
        "Инвестиционный раунд",
        "Серьёзный B2B-блок",
      ]
    },
  ];
  return (
    <div>
      <SectionTitle sub="Поэтапный план от MVP до полноценной экосистемы">Роадмап</SectionTitle>
      {phases.map(({ phase, time, title, color, tasks }) => (
        <Card key={phase}>
          <div style={{ display: "flex", gap: 16, alignItems: "center", marginBottom: 14 }}>
            <div style={{ background: color, borderRadius: 6, padding: "4px 12px", fontSize: 12, fontWeight: 700, color: "#000" }}>{phase}</div>
            <div style={{ color: muted, fontSize: 13 }}>{time}</div>
            <div style={{ color: "#fff", fontWeight: 600, fontSize: 15 }}>{title}</div>
          </div>
          {tasks.map(t => (
            <div key={t} style={{ display: "flex", gap: 10, marginBottom: 8, fontSize: 13, color: muted }}>
              <span style={{ color, flexShrink: 0 }}>▸</span>{t}
            </div>
          ))}
        </Card>
      ))}
    </div>
  );
}
