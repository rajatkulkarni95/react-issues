# Bug: Report bug to react team

> Issue #32239 - Created on 1/28/2025

> Original URL: https://github.com/facebook/react/issues/32239

## Description

<!--
  Please provide a clear and concise description of what the bug is. Include
  screenshots if needed. Please test using the latest version of the relevant
  React packages to make sure your issue has not already been fixed.
-->

React version:
18.2.0
## Steps To Reproduce

1. Have a code who looks like
```
const fetchReports = async (pageNum) => {
        if (loading) return;
        setLoading(true);
        try {
            const response = await fetch(`http://localhost:8000/reports/list?page=${pageNum}`);
            const data = await response.json();
            
            if (data.data.length === 0) {
                setHasMore(false);
            }

            setReports(data.data);
        } catch (error) {
            console.log(error);
            setError("An error occurred");
        } finally {
            setLoading(false);
        }
    }
```
I will explain my situation. I'm using Laravel to manage the backend and actually the controller returns `Report::orderBy('created_at', 'desc')->paginate(10);` who is supposed to return 10 reports (link ends with `?page=1`)

I see that error when I'm using setReports.
If you don't see what Report mean it's a model (an object) who is stored in database and there is the migration (a php code to create table)

```
        Schema::create('sanctions', function (Blueprint $table) {
            $table->id();
            $table->foreignIdFor(Player::class, 'player');
            $table->timestamp('end');
            $table->string('reason');
            $table->string('type');
            $table->foreignIdFor(User::class, 'moderator');
            $table->foreignIdFor(Report::class, 'report')->nullable();
            $table->timestamps();
        });
```


## The current behavior
Print ```hook.js:608 Warning: Internal React error: Expected static flag was missing. Please notify the React team. Error Component Stack
    at ReportTable (ReportTable.jsx:4:25)
    at div (<anonymous>)
    at div (<anonymous>)
    at div (<anonymous>)
    at div (<anonymous>)
    at main (<anonymous>)
    at div (<anonymous>)
    at div (<anonymous>)
    at AuthenticatedLayout (AuthenticatedLayout.jsx:8:47)
    at NewReports (NewReports.jsx:6:38)```

in console but it looks working


## The expected behavior
Print an other error or work





If you want to reproduce this bug on your computer you firstly have to setup a laravel app (using composer command or laravel command). Everything is explained here https://laravel.com/docs/11.x/installation#installing-php

Dont forget that during laravel app it will ask you to use jetstream (u say  yes) and you select react with Inertia. Then PHPUnit
Then after everything installed you may go into .env and put your mysql credentials (if u are using it).

Now you can run the command `php artisan make:model Report -m` it will create you 2 files
`app/Models/Report.php`

For my part there isn't anything inside because I don;t really need (reports aren't created by my laravel app). So it will looks like 
```
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Report extends Model
{
    //
}
```

Now you have a second file created in database/migrations which contains create_reports_table.php

You have to put this inside

```
return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        Schema::create('reports', function (Blueprint $table) {
            $table->id();
            $table->integer('reporter');
            $table->integer('reported');
            $table->integer('moderator')->nullable();
            $table->string('reason');
            $table->integer('state')->default(0);
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::dropIfExists('reports');
    }
};
```

Now we will go into routes/web.php (you can comment the last require line)
You will have a route who will return 10 reports.

You will make a function (take example at Welcome render)
But who will return `Report::orderBy('created_at', 'desc')->paginate(10);` (don't forget that Report comes from App\Models\Report)
Then you can give him a name with ->('name');

Let's talk about react !
You have to delete all content of the Welcome function located at `resources/js/Page/Welcome.jsx` and set you a basic page with that
```
    const [page, setPage] = useState(1);
    const [loading, setLoading] = useState(false);
    const [reports, setReports] = useState([]);
    const [error, setError] = useState('');
    const [hasMore, setHasMore] = useState(true);

    const fetchPosts = async (pageNum) => {
        if (loading) return;
        setLoading(true);
        try {
            const response = await fetch(route('reports.list', { page: pageNum }));
            const data = await response.json();
            
            if (data.data.length === 0) {
                setHasMore(false);
            }

            setReports(data.data);
        } catch (error) {
            console.log(error);
            setError("An error occurred");
        } finally {
            setLoading(false);
        }
    }

    useEffect(() => {
        fetchPosts(page);
    }, [page]);
```

Do you remember about the route you named before ? You have to put the name here  const response = await fetch(route('reports.list', { page: pageNum }));

Dont forget to create table with `php artisan migrate` at the root of your project and start a temporally web server with `php artisan serve`

Now in a new window you have to run `npm i` and then `npm run dev`

Phew I thinks that's all
