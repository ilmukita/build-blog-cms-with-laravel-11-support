# C01E011P001 - Membuat Migrasi, Model, dan Seeder untuk Data Tag

## Create Migration

```bash
php artisan make:migration create_tags_table
```

database\migrations\xxx_xx_xx_xxxxxx_create_tags_table.php

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        Schema::create('tags', function (Blueprint $table) {
            $table->id();
            $table->string('title', 60);
            $table->string('slug');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::dropIfExists('tags');
    }
};
```

### Migrate Tabel

```bash
php artisan migrate
# or
php artisan migrate:fresh --seed
```

## Create Model

```bash
php artisan make:model Tag
```

app\Models\Tag.php

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Tag extends Model
{
    use HasFactory;

    protected $fillable = [
        'title',
        'slug',
    ];
}
```

## Create Seeder

```bash
php artisan make:seeder TagTableSeeder
```

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;
use Illuminate\Support\Str;

class TagTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     */
    public function run(): void
    {
        $tagsDummies = require_once database_path("dummies/TagDummy.php");

        $inserts = [];

        foreach ($tagsDummies as $tagDummy) {
            $inserts[] = [
                'title' => $tagDummy,
                'slug' => Str::slug($tagDummy),
                'created_at' => now(),
                'updated_at' => now()
            ];
        }

        DB::table('tags')->insert($inserts);
    }
}
```

database\seeders\TagTableSeeder.php

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
   public function run(): void
   {

      $this->call([
         // another code ...
         TagTableSeeder::class,
      ]);
   }
}

```

### Running Seeders

```bash
php artisan db:seed

#by class
php artisan db:seed --class=TagTableSeeder
```

### Tag Dummy

database\dummies\TagDummy.php

```php
<?php

return [
    'ilmukita',
    'ilmukita youtube',
    'laravel blog',
    'laravel tutorial',
    'laravel 11',
    'laravel cms',
    'laravel bootstrap',
    'build blog with laravel',
    'laravel blog development',
    'laravel blog project',
    'laravel blog tutorial',
    'laravel blog website',
    'laravel add bootstrap',
    'Install Bootstrap CSS',
    'Tutorial Laravel 11 Blog CMS',
    'Content Management System',
    'Build Blog CMS with Laravel 11',
    'laravel 11 project',
    'laravel 11 new features',
    'laravel 11 tutorial',
    'laravel blog with admin panel',
    "youtube",
    "laravel 11",
    "php 8.2",
    "programming",
    "tutorial",
    "coding",
    "web development",
    "javascript",
    "python",
    "backend",
    "language",
    "java",
    "oop",
    "development",
    "html",
    "css",
    "web design",
    "mysql",
    "database",
    "query",
    "react",
    "frontend",
    "library",
    "angular",
    "framework",
    "node.js",
    "server",
    "ruby",
    "git",
    "version control",
    "repository",
    "github",
    "code hosting",
    "docker",
    "containerization",
    "phpstorm",
    "ide",
    "laragon",
    "local server",
    "environment",
    "bootstrap",
    "mongodb",
    "nosql",
    "sass",
    "preprocessor",
    "jenkins",
    "continuous integration",
    "automation",
    "typescript",
    "superset",
    "wordpress",
    "cms",
    "blogging",
    "laravel",
    "symfony",
    "flask",
    "microframework",
    "spring boot",
    "android",
    "mobile",
    "ios",
    "kotlin",
    "swift",
    "unity",
    "game",
    "unreal engine",
    "cplusplus",
    "frontend development",
    "web programming",
    "object oriented",
    "mobile app",
    "version control system",
    "web framework",
    "server-side scripting",
    "code repository",
    "web hosting",
    "container orchestration",
    "integrated development environment",
    "local development",
    "backend development",
    "database management",
    "data manipulation",
    "test automation",
    "continuous delivery",
    "static site generator",
    "content management system",
    "game development",
    "programming language",
    "software development",
    "web application",
    "software engineering",
    "responsive web design",
    "cloud computing",
    "serverless computing",
    "microservices architecture",
    "network programming",
    "desktop application",
    "graphical user interface",
    "mobile development",
    "mobile operating system",
    "mobile application development",
    "cross-platform development",
    "machine learning",
    "data science",
    "artificial intelligence",
    "blockchain technology",
    "cloud storage",
    "data visualization",
    "database administration",
    "web security",
    "network security",
    "cybersecurity measures",
    "algorithm optimization",
    "coding standards",
    "debugging techniques",
    "software architecture",
    "software testing",
    "quality assurance",
    "user experience design",
    "user interface design",
    "agile methodology",
    "scrum framework",
    "project management",
    "collaborative development",
    "open-source software",
    "version control platform",
    "continuous integration tool",
    "continuous deployment tool",
    "web development framework",
    "server-side scripting language",
    "front-end framework",
    "programming language syntax",
    "integrated development environment",
    "software development lifecycle",
    "mobile application framework",
    "game engine",
    "graphics rendering engine",
    "computer graphics programming",
    "game physics simulation",
    "game design principles",
    "object-oriented programming",
    "functional programming paradigm",
    "imperative programming style",
    "declarative programming approach",
    "concurrent programming",
    "parallel computing",
    "distributed systems",
    "network protocols",
    "data transmission",
    "encryption techniques",
    "authentication methods",
    "access control mechanisms",
    "data compression algorithms",
    "error handling strategies",
    "performance optimization",
    "code refactoring techniques",
    "software documentation",
    "unit testing frameworks",
    "test-driven development",
    "behavior-driven development",
    "agile project management",
    "kanban methodology",
    "sprint planning",
    "user story mapping",
    "pair programming",
    "code review process",
    "continuous improvement",
    "community-driven development",
    "open-source contribution",
    "technical debt management",
    "code versioning system",
    "collaborative coding platforms",
    "automated deployment pipelines",
    "web content management system",
    "content creation platforms",
    "content distribution networks",
    "search engine optimization",
    "digital marketing strategies",
    "social media integration",
    "e-commerce platforms",
    "online payment gateways",
    "customer relationship management",
    "business process automation",
    "enterprise resource planning",
    "supply chain management",
    "data analytics tools",
    "business intelligence software",
    "cloud-based solutions",
    "cybersecurity frameworks",
    "network monitoring tools",
    "incident response procedures",
    "risk assessment methodologies",
    "compliance standards",
    "privacy regulations",
    "data protection laws",
    "encryption standards",
    "identity management systems",
    "access control policies",
    "intrusion detection systems",
    "firewall configurations",
    "vulnerability scanning",
    "penetration testing",
    "security awareness training",
    "emergency response planning",
    "disaster recovery strategies",
    "backup and restoration procedures",
    "high availability architectures",
    "fault tolerance mechanisms",
    "load balancing algorithms",
    "performance monitoring tools",
    "resource optimization techniques",
    "scalability solutions",
    "cloud migration strategies",
    "hybrid cloud environments",
    "multi-cloud deployments",
    "serverless computing models",
    "microservices architecture",
    "container orchestration platforms",
    "continuous integration/continuous deployment pipelines",
    "automated testing frameworks",
    "agile software development methodologies",
    "devops practices",
    "site reliability engineering",
    "infrastructure as code",
    "configuration management tools",
    "monitoring and logging solutions",
    "incident response automation",
    "security as code",
    "cloud-native development",
    "serverless computing",
    "microservices architecture",
    "container orchestration",
    "continuous integration and continuous deployment",
    "automated testing",
    "agile software development",
    "devops practices",
    "site reliability engineering",
    "infrastructure as code",
    "configuration management",
    "monitoring and logging",
    "incident response automation",
    "security as code",
    "cloud-native development"
];
```

## Ref

- [Eloquent: Getting Started - Laravel 11.x - The PHP Framework For Web Artisans](https://laravel.com/docs/11.x/eloquent#generating-model-classes)

- [Installation - Laravel 11.x - The PHP Framework For Web Artisans](https://laravel.com/docs/11.x/installation#databases-and-migrations)

- https://laravel.com/docs/11.x/eloquent-factories

- https://fakerphp.org/
