# Minha configuração Rails 7

Esse README visa centralizar os passos da configuração de novos projetos em Rails 7.

Obs: Os passos de instalação são de critério individual, eu recomendo o uso do tutorial disponível no [GoRails](https://gorails.com/setup/ubuntu/22.04)



### Criando o projeto

Dentro da pasta onde deseja criar seu projeto, execute o seguinte comando:

```bash
rails new meuprojeto
```

Para realizar as próximas etapas, é necessário estar dentro da pasta raiz do projeto <strong>meuprojeto</strong>, para isso execute o seguinte comando:

```bash
cd meuprojeto
```

Uma etapa importante é a configuração do <strong>time_zone</strong> do projeto, para isso, vamos acessar o arquivo <strong>config/application.rb</strong>, nele vamos adicionar a configuração abaixo:

```ruby
require_relative "boot"
require "rails/all"
Bundler.require(*Rails.groups)

module Myexamples
  class Application < Rails::Application    
    config.load_defaults 7.0   	
    config.time_zone = "La Paz" # Configuração do Time Zone   	
  end
end
```

###### Para que as alterações se tornem vigentes, é necessário reiniciar o serviço. 

Para encontrar o <strong>config.time_zone</strong> você pode acessar a [documentação](https://api.rubyonrails.org/classe			s/ActiveSupport/TimeZone.html) e encontrar o sua referência.



#### Tradução

Para adicionarmos o nosso idioma ao projeto, devemos adicionar uma nova configuração, e para isso vamos acessar novamente o arquivo <strong>config/application.rb</strong> e adicionar o código abaixo:

```ruby
require_relative "boot"
require "rails/all"
Bundler.require(*Rails.groups)

module Myexamples
  class Application < Rails::Application    
    config.load_defaults 7.0   	
    config.time_zone = "La Paz" 		  # Configuração do Time Zone
    config.i18n.default_locale = :'pt-BR' # Configuração do idioma padrão
  end
end
```

Para finalizar a configuração de idioma, vamos criar um arquivo <strong>pt-BR.yml</strong> na pasta <strong>config/locales</strong> e adicionar as chaves de tradução:

```yml
---
pt-BR:
  activerecord:
    errors:
      messages:
        record_invalid: 'A validação falhou: %{errors}'
        restrict_dependent_destroy:
          has_one: Não é possível excluir o registro pois existe um %{record} dependente
          has_many: Não é possível excluir o registro pois existem %{record} dependentes
  date:
    abbr_day_names:
    - dom
    - seg
    - ter
    - qua
    - qui
    - sex
    - sáb
    abbr_month_names:
    -
    - jan
    - fev
    - mar
    - abr
    - mai
    - jun
    - jul
    - ago
    - set
    - out
    - nov
    - dez
    day_names:
    - domingo
    - segunda-feira
    - terça-feira
    - quarta-feira
    - quinta-feira
    - sexta-feira
    - sábado
    formats:
      default: "%d/%m/%Y"
      long: "%d de %B de %Y"
      short: "%d de %B"
    month_names:
    -
    - janeiro
    - fevereiro
    - março
    - abril
    - maio
    - junho
    - julho
    - agosto
    - setembro
    - outubro
    - novembro
    - dezembro
    order:
    - :day
    - :month
    - :year
  datetime:
    distance_in_words:
      about_x_hours:
        one: aproximadamente %{count} hora
        other: aproximadamente %{count} horas
      about_x_months:
        one: aproximadamente %{count} mês
        other: aproximadamente %{count} meses
      about_x_years:
        one: aproximadamente %{count} ano
        other: aproximadamente %{count} anos
      almost_x_years:
        one: quase %{count} ano
        other: quase %{count} anos
      half_a_minute: meio minuto
      less_than_x_seconds:
        one: menos de %{count} segundo
        other: menos de %{count} segundos
      less_than_x_minutes:
        one: menos de um minuto
        other: menos de %{count} minutos
      over_x_years:
        one: mais de %{count} ano
        other: mais de %{count} anos
      x_seconds:
        one: "%{count} segundo"
        other: "%{count} segundos"
      x_minutes:
        one: "%{count} minuto"
        other: "%{count} minutos"
      x_days:
        one: "%{count} dia"
        other: "%{count} dias"
      x_months:
        one: "%{count} mês"
        other: "%{count} meses"
      x_years:
        one: "%{count} ano"
        other: "%{count} anos"
    prompts:
      second: Segundo
      minute: Minuto
      hour: Hora
      day: Dia
      month: Mês
      year: Ano
  errors:
    format: "%{attribute} %{message}"
    messages:
      accepted: deve ser aceito
      blank: não pode ficar em branco
      confirmation: não é igual a %{attribute}
      empty: não pode ficar vazio
      equal_to: deve ser igual a %{count}
      even: deve ser par
      exclusion: não está disponível
      greater_than: deve ser maior que %{count}
      greater_than_or_equal_to: deve ser maior ou igual a %{count}
      in: deve estar em %{count}
      inclusion: não está incluído na lista
      invalid: não é válido
      less_than: deve ser menor que %{count}
      less_than_or_equal_to: deve ser menor ou igual a %{count}
      model_invalid: 'A validação falhou: %{errors}'
      not_a_number: não é um número
      not_an_integer: não é um número inteiro
      odd: deve ser ímpar
      other_than: deve ser diferente de %{count}
      present: deve ficar em branco
      required: é obrigatório(a)
      taken: já está em uso
      too_long:
        one: 'é muito longo (máximo: %{count} caracter)'
        other: 'é muito longo (máximo: %{count} caracteres)'
      too_short:
        one: 'é muito curto (mínimo: %{count} caracter)'
        other: 'é muito curto (mínimo: %{count} caracteres)'
      wrong_length:
        one: não possui o tamanho esperado (%{count} caracter)
        other: não possui o tamanho esperado (%{count} caracteres)
    template:
      body: 'Por favor, verifique o(s) seguinte(s) campo(s):'
      header:
        one: 'Não foi possível gravar %{model}: %{count} erro'
        other: 'Não foi possível gravar %{model}: %{count} erros'
  helpers:
    select:
      prompt: Por favor selecione
    submit:
      create: Criar %{model}
      submit: Salvar %{model}
      update: Atualizar %{model}
  number:
    currency:
      format:
        delimiter: "."
        format: "%u %n"
        precision: 2
        separator: ","
        significant: false
        strip_insignificant_zeros: false
        unit: R$
    format:
      delimiter: "."
      precision: 3
      separator: ","
      significant: false
      strip_insignificant_zeros: false
    human:
      decimal_units:
        format: "%n %u"
        units:
          billion:
            one: bilhão
            other: bilhões
          million:
            one: milhão
            other: milhões
          quadrillion:
            one: quatrilhão
            other: quatrilhões
          thousand: mil
          trillion:
            one: trilhão
            other: trilhões
          unit: ''
      format:
        delimiter: ''
        precision: 3
        significant: true
        strip_insignificant_zeros: true
      storage_units:
        format: "%n %u"
        units:
          byte:
            one: Byte
            other: Bytes
          eb: EB
          gb: GB
          kb: KB
          mb: MB
          pb: PB
          tb: TB
    percentage:
      format:
        delimiter: "."
        format: "%n%"
    precision:
      format:
        delimiter: "."
  support:
    array:
      last_word_connector: " e "
      two_words_connector: " e "
      words_connector: ", "
  time:
    am: ''
    formats:
      default: "%a, %d de %B de %Y, %H:%M:%S %z"
      long: "%d de %B de %Y, %H:%M"
      short: "%d de %B, %H:%M"
    pm: ''
```



### Simple Form

Adicione ao seu arquivo Gemfile:	

````ruby
gem "simple_form"
````

Após adicionar o código acima no seu Gemfile, execute esse comando na raiz do seu projeto:

```bash
bundle install
```

Para executar o gerador de "views" do Simple Form execute o comando abaixo, na raiz do seu projeto:

Obs:  É enviado o parâmetro "-- bootstrap" para adicionar o arquivo simple_form.boostrap.rb que é da própria gem para facilitar o uso do Bootstrap

```bash
rails generate simple_form:install --bootstrap
```



#### Tradução Simple Form

Como já adicionamos a configuração do idioma no arquivo <strong>config/application.rb</strong>,  vamos apenas criar um arquivo <strong>simple_form.pt-BR.yml</strong> dentro de <strong>config/locales/</strong>, copie e cole dentro do arquivo que acabou de criar:

```yml
pt-BR:
  simple_form:
    "yes": 'Sim'
    "no": 'Não'
    required:
      text: 'obrigatório'
      mark: '*'
      # You can uncomment the line below if you need to overwrite the whole required html.
      # When using html, text and mark won't be used.
      # html: '<abbr title="required">*</abbr>'
    error_notification:
      default_message: "Alguns erros foram encontrados, por favor verifique:"
    # Labels and hints examples
    # labels:
    #   password: 'Password'
    #   user:
    #     new:
    #       email: 'E-mail para efetuar o sign in.'
    #     edit:
    #       email: 'E-mail.'
    # hints:
    #   username: 'User name to sign in.'
    #   password: 'No special characters, please.'
```



### Pagy

Adicione ao seu arquivo Gemfile:

```ruby
gem "pagy"
```

Após adicionar o código acima no seu Gemfile, execute esse comando na raiz do seu projeto:

```bash
bundle install
```



##### Após executar o comando acima, teremos que configurar a Gem no projeto.

Adicione o código abaixo no arquivo <strong>app/controllers/application_controller.rb</strong>:

```ruby
include Pagy::Backend
```

Adicione o código abaixo no arquivo <strong>app/helpers/application_helper.rb</strong>:

```ruby
include Pagy::Frontend
```



##### Exemplo do uso da Gem Pagy:

Vamos imaginar que temos um Model Produto, dentro do método onde gostaríamos adicionar uma paginação, nosso código deve estar próximo do exemplo abaixo:

Obs:  O código abaixo é um exemplo usando apenas a Gem Pagy

```ruby
def index
  @pagy, @produtos = pagy(Produto.all)
end
```

Para configurações mais avançadas, acesse a documentação da Gem [Pagy](https://github.com/ddnexus/pagy)



#### Tradução Pagy



### Ransack 







    