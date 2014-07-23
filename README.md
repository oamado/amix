Amix
====

Enable reporting to Newrelic through statman for Plug based web servers

##Setting Up 
###Installation

1. Add amix to your `mix.exs` dependencies:

    ```elixir
    def deps do
      [
      {:amix, github: "arielze/amix"}
      ]
    end
    ```
2. Add Amix.Supervisor to your supervision tree
  ```elixir
    children = [
      supervisor(Amix.Supervisor, [])
    ]
    ```
3. Add Amix.Wrapper before the :math Plug
    ```elixir
    defmodule MyApp do
      import Plug.Conn
      use Application
      use Plug.Router

      plug Amix.Wrapper, [] 
      plug :match
      plug :dispatch
```

###Configuration

1. Add Newrelic application to your app.conf file
  ```elixir
 [
   newrelic: [
     application_name: 'MyApp Name', 
     license_key: '1234567890'
   ]
 ]  
 ```

 And voila, you should see transactions in you application overview on Newrelic.
 the connector also reports responses with code >= 400 as error to Newrelic

if you find yourself struggling with lhttpc compilation errors, you should remove non standard characters from this extension Author name.

