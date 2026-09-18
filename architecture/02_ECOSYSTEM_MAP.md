# خريطة المنظومة ومسارات الحزم (Ecosystem Map)

تتألف منظومة أوغاريت من مجموعة حزم مركزية متكاملة تتوزع في بنية هرمية واضحة:

```mermaid
graph TD
    Kernel[Ugarit Framework <br/> Heritage Namespace] --> CLI[Scribe CLI Engine]
    Kernel --> Prompts[Ugarit Prompts]
    Kernel --> Boost[Ugarit Boost AI Engine]
    
    Installer[Ugarit Installer CLI <br/> ugarit new] --> Kernel
    Installer --> StarterKits[Starter Kits <br/> React / Vue / Svelte / Livewire]
    
    CustomModules[Customization Pillars <br/> i18n / Identity / Storage / Geography] --> Kernel
    ReferenceSources[Sources Catalog <br/> LevantC Modules] -. Reference & Blueprints .-> CustomModules
```

---

## 1. الحزم المركزية الأساسية (Core Packages)
* **`ugarit/framework`** (`j:\ugarit\framework`):
  النواة الشاملة التي تدير الحاويات (Container)، التوجيه (Routing)، قواعد البيانات (Database/ORM)، الأحداث (Events)، والوسائط، وتستخدم مساحة الأسماء `Heritage\...`.
* **`ugarit/installer`** (`j:\ugarit\installer`):
  أداة إنشاء وإعداد تطبيقات أوغاريت الجديدة عبر سطر الأوامر (`ugarit new`).
* **`ugarit/prompts`** (`j:\ugarit\prompts`):
  نظام المحثات والواجهات التفاعلية في سطر الأوامر.
* **`ugarit/boost`** (`j:\ugarit\boost`):
  محرك دعم وتوجيه الذكاء الاصطناعي ووكلاء البرمجة ومخدمات بروتوكول سياق النموذج (MCP).
* **`ugaritco/pest-plugin-ugarit`** (`j:\ugarit\pest-plugin-ugarit`):
  إضافة إطار Pest لدعم بيئة أوغاريت وتشغيل الاختبارات التلقائية.

---

## 2. قوالب البداية الرسمية (Starter Kits)
* `react-starter-kit` (و `blank-react-starter-kit`)
* `vue-starter-kit` (و `blank-vue-starter-kit`)
* `svelte-starter-kit` (و `blank-svelte-starter-kit`)
* `livewire-starter-kit` (و `blank-livewire-starter-kit`)
* `api-starter-kit`
