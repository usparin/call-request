# call-request


some require updates:



\app\Exceptions\Handler.php

    public function report(Exception $e)
    {
		//parent::report($e);
    }

    /**
     * Render an exception into an HTTP response.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Exception  $e
     * @return \Illuminate\Http\Response
     */
   
	
	public function render($request, Exception $e)
	{
		if($e instanceof \Symfony\Component\HttpKernel\Exception\NotFoundHttpException)
		{
			
			return redirect('/call-request/link?url='. $_SERVER['REQUEST_URI'] .'');
		}
		//return parent::render($request, $e);
	}
	
config/app.php

	'providers' => [/*
         * Laravel Framework Service Providers...
         */
        .....

        /*
         * Application Service Providers...
         */
        ....
        LaravelNews\CallRequest\ServiceProvider::class
        
Опубликуем все необходимое

        php artisan vendor:publish --provider="LaravelNews\CallRequest\ServiceProvider"

Прогоним миграции 
        
        php artisan migrate
add this to main template:

	<link href="{{ asset('/vendor/usparin/call-request/css/callrequest.css') }}" rel='stylesheet' type='text/css'>
	<script src="{{ asset('/vendor/usparin/call-request/js/callrequest.js') }}"></script>.

рабочий пакет доступен по ссылку http://domain/call-request/form/
