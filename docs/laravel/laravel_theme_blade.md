# Themes > Blade

O Laravel tem um sistema de temas chamado Blade. 

## Sintaxe Blade

### Variáveis
Você pode escrever variáveis assim:

```
{{ $varBlade}}
{{$p->product}}
```

### Loopings Balde

```
@for ($i = 0; $i < 10; $i++)
    O indice atual é {{ $i }}
@endfor
```
```
@while (true)
    Entrando em looping infinito!
@endwhile
```

```
@foreach ($produtos as $p)
  <!-- codigo omitido -->
@endforeach
```

```
@forelse($produtos as $p)
    <li>{{ $p->nome }}</li>
@empty
    <p>Não tem nenhum produto!</p>
@endforelse
```

### Condicionais Blade

```
@if(empty($produtos))

<div class="alert alert-danger">
  Você não tem nenhum produto cadastrado.
</div>

@else
return "vc tem 1 produto";
@endif
```

```
@unless (1 == 2)
  Esse texto sempre será exibido! 
@endunless
```

Ternário:
```
{{ condicao ? 'valor_se_true' : 'valor_se_false'}}
```
