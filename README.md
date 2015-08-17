# FNA-Style-Guide-iOS-pt-BR

The Objective-C Style Guide utilizado por Fábio Nogueira

## Table of Contents

* [Linguagem](#linguagem)
* [Quando utilizar ponto](#quando-utilizar-ponto)
* [Organização de código](#organização-de-código)
* [Espaços](#espaços)
* [Padrão para declarações](#padrão-para-declarações)
* [Nomenclatura](#nomenclatura)
* [Métodos](#métodos)
* [Variáveis](#variáveis)
* [Propriedades](#propriedades)
* [Sintaxe Dot-Notation](#sintaxe-dot-notation)
* [Literais](#literais)
* [Tipos enumerados](#tipos-enumerados)
* [Sintaxe Case](#sintaxe-case)
* [Booleanos](#booleanos)
* [Métodos inicializadores](#métodos-inicializadores)
* [Métodos Construtores de classes ](#métodos-construtores-de-classes)
* [Funções CGRect](#funções-cgrect)
* [Singletons](#singletons)
* [TableView](#tableview)


## Linguagem

O Inglês deve ser utilizado. Português será aceito apenas para dados de modelo.

## Quando utilizar ponto

Utilize o ponto **sempre** quando for acessar e alterar uma propriedade. Em todos os outros casos é recomendo a utilização dos colchetes.

**Exemplo correto:**

```objc
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**Inadequado:**

```objc
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```


## Organização de Código

Use `#pragma mark -` para organizar as propriedades e métodos por categorias.

```objc
#pragma mark - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}

#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}

#pragma mark - Public

- (void)publicMethod {}

#pragma mark - Private

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - NSObject

- (NSString *)description {}
```

## Espaços

* Utilizar indentação com 4 espaços. Nunca utilizar tabs para indentação. Altere a propriedade do Xcode para alterar o tab por 4 espaços.
* Chaves de métodos (`if`/`else`/`switch`/`while`, etc) sempre será aberta na mesma linha e fechadas em uma nova linha.

**Exemplo correto:**

```objc
if (user.isHappy) {
  //Do something
} else {
  //Do something else
}
```

**Inadequado:**

```objc
if (user.isHappy)
{
    //Do something
}
else {
    //Do something else
}
```

## Padrão para declarações

* Não utilizar a formatação default do Xcode para métodos com chamadas parecidas com o exemplo abaixo.

**Exemplo correto:**

```objc
// blocks are easily readable
[UIView animateWithDuration:1.0 animations:^{
  // something
} completion:^(BOOL finished) {
  // something
}];
```

**Inadequado:**

```objc
// colon-aligning makes the block indentation hard to read
[UIView animateWithDuration:1.0
                 animations:^{
                     // something
                 }
                 completion:^(BOOL finished) {
                     // something
                 }];
```

* Não deverá ter linha vazia acima das declarações condicionais

```objc
- (void)methodA {
	BOOL varA = YES;
	if (varA) {
	}
}
```

* Exemplos de declaração quando utilizado Arrays e Dictionarys

```objc
    [mapping addAttributeMappingsFromArray:@[
        @"codigo",
        @"nome",
        @"idade",
        @"profissao",
        @"religiao",
        @"recomendacao"]
    ];
```

## Nomenclatura

Convenção de nomes da Apple devem ser respeitadas sempre que possível, especialmente aqueles relacionados com as [regras de gerênciamento de memória](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html) ([NARC](http://stackoverflow.com/a/2865194/340508)).

* Nomes de propriedades e métodos longos, descritivos são bem aceitos.
Métodos podem ser escritos parecendo verdadeiras frases de objetivos.

**Exemplo correto:**

```objc
UIButton *settingsButton;
```

**Inadequado:**

```objc
UIButton *setBut;
```


* Constantes devem conter um espaço após o * da atribuição.

**Exemplo correto:**


```objc
const CGFloat * components = CGColorGetComponents(color.CGColor);

```

* Constantes devem ser camel-case com todas as palavras e prefixos relacionados a classe e depois seu objetivo.

**Exemplo correto:**

```objc
static NSTimeInterval const RWTTutorialViewControllerNavigationFadeAnimationDuration = 0.3;
```

**Inadequado:**

```objc
static NSTimeInterval const fadetime = 1.7;
```

* Propriedades devem ser camel-case e começando com a primeira letra minúscula.

**Exemplo correto:**

```objc
@property (strong, nonatomic) NSString *descriptiveVariableName;
```

### Chamadas de propriedades

As propriedades devem ser chamadas utiizando o `self.`. Apenas não há necessidade quando a propriedades for uma criada localmente em algum método. 

Váriavéis locais não devem conter `self.` 

## Métodos

* Em assinaturas de método, deve haver um espaço após o tipo de método (- / + símbolo). 
* Deve haver um espaço entre os segmentos de método. 
* Sempre incluir uma palavra-chave e ser descritivo com a palavra antes do argumento que descreve o argumento.
* Não utilização da palavra "and" para relacionar outro parâmetro de um método

**Exemplo correto:**

```objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
- (id)viewWithTag:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
```

**Inadequado:**

```objc
-(void)setT:(NSString *)text i:(UIImage *)image;
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
- (id)taggedView:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
- (instancetype)initWith:(int)width and:(int)height;  // Never do this.
```

Métodos privados devem possui o préfixo `_` antes do nome

```objc
- (void)_privateMethod {}
```

## Variáveis

**Exemplo correto:**

```objc
@interface RWTTutorial : NSObject

@property (strong, nonatomic) NSString *tutorialName;

@end
```

**Inadequado:**

```objc
@interface RWTTutorial : NSObject {
  NSString *tutorialName;
}
```


## Propriedades

Atributos de propriedade deve ser explicitamente listados, e vai ajudar novos programadores ao ler o código.
A ordem de propriedades deve ser de armazenamento, em seguida, atomicidade, o que é consistente com o código gerado automaticamente ao conectar elementos da interface de Interface Builder.

**Exemplo correto:**

```objc
@property (weak, nonatomic) IBOutlet UIView *containerView;
@property (strong, nonatomic) NSString *tutorialName;
```

**Inadequado:**

```objc
@property (nonatomic, weak) IBOutlet UIView *containerView;
@property (nonatomic) NSString *tutorialName;
```

Propriedades com valores mutáveis (por exemplo NSString) deve preferir `copy` em vez de` strong`.
Por quê? Mesmo se você declarou uma propriedade como `NSString` alguém pode passar em uma instância de um` NSMutableString` e, em seguida, alterá-lo sem você perceber isso. 

**Exemplo correto:**

```objc
@property (copy, nonatomic) NSString *tutorialName;
```

**Inadequado:**

```objc
@property (strong, nonatomic) NSString *tutorialName;
```

## Sintaxe Dot-Notation

Use Dot syntax apenas para acessar propriedades e não realizar chamadas de métodos. Leia mais [aqui](https://developer.apple.com/library/ios/documentation/cocoa/conceptual/ProgrammingWithObjectiveC/EncapsulatingData/EncapsulatingData.html)

**Exemplo correto:**

```objc
NSInteger arrayCount = [self.array count];
view.backgroundColor = [UIColor orangeColor];
```

**Inadequado:**

```objc
NSInteger arrayCount = self.array.count;
[view setBackgroundColor:[UIColor orangeColor]];
```

## Literais

`NSString`, `NSDictionary`, `NSArray`, e `NSNumber` devem ser utilizados de forma literal.

**Exemplo correto:**

```objc
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingStreetNumber = @10018;
```

**Inadequado:**

```objc
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];
```

Constantes são preferidos sobre in-line strings literais ou números, já que permitem a fácil reprodução de variáveis comumente usadas e podem ser rapidamente alterados sem a necessidade de localizar e substituir. Constantes devem ser declarados como `constantes static` e não` # define`s a menos que explicitamente sendo usado como uma macro.

**Exemplo correto:**

```objc
static NSString * const RWTAboutViewControllerCompanyName = @"RayWenderlich.com";

static CGFloat const RWTImageThumbnailHeight = 50.0;
```

**Inadequado:**

```objc
#define CompanyName @"RayWenderlich.com"

#define thumbnailHeight 2
```

## Tipos enumerados

Ao usar enums, recomenda-se a usar a nova especificação do tipo fixo subjacente porque tem forte verificação de tipo e conclusão de código. O SDK inclui agora uma macro para facilitar e incentivar a utilização de tipos subjacentes fixos: NS_ENUM ()

**For Example:**

```objc
typedef NS_ENUM(NSInteger, RWTLeftMenuTopItemType) {
  RWTLeftMenuTopItemMain,
  RWTLeftMenuTopItemShows,
  RWTLeftMenuTopItemSchedule
};
```

Você também pode fazer atribuições de valores explícitos 

```objc
typedef NS_ENUM(NSInteger, RWTGlobalConstants) {
  RWTPinSizeMin = 1,
  RWTPinSizeMax = 5,
  RWTPinCountMin = 100,
  RWTPinCountMax = 500,
};
```

**Inadequado:**

```objc
enum GlobalConstants {
  kMaxPinSize = 5,
  kMaxPinCount = 500,
};
```


## Sintaxe case

Chaves não são necessários para instruções case, a menos imposto pelo compilador.
Quando um caso contém mais de uma linha, deve ser adicionado chaves.

```objc
switch (condition) {
  case 1:
    // ...
    break;
  case 2: {
    // ...
    // Multi-line example using braces
    break;
  }
  case 3:
    // ...
    break;
  default: 
    // ...
    break;
}

```

## Booleanos

`nil` é interpretado como `NO` portanto não é necessário compará-lo em condições. Nunca compare algo diretamente com `YES` porque `YES` é definido como 1 e um `BOOL` pode ser de até 8 bits.

Isso permite uma maior consistência entre os arquivos e maior clareza visual.

**Exemplo correto:**

```objc
if (!someObject) {
}
```

**Inadequado:**

```objc
if (someObject == nil) {
}
```

-----

**Para um `BOOL`, temos dois exemplos:**

```objc
if (isAwesome)
if (![someObject boolValue])
```

**Inadequado:**

```objc
if (isAwesome == YES) // Nunca faça isso.
if ([someObject boolValue] == NO)
```

-----

Se o nome de uma propriedade do tipo `BOOL` é expresso como um adjetivo, a propriedade pode omitir o prefixo "is", mas deve continuar especificando o nome convencional para o metodo de acesso `get`. Exemplo:

```objc
@property (assign, getter=isEditable) BOOL editable;
```

## Métodos inicializadores

Utilizar convenção padrão da apple para a inicialização e sempre utilizar instancetype ao invés de id

```objc
- (instancetype)init {
  self = [super init];
  if (self) {
    // ...
  }
  return self;
}
```


## Métodos construtores de classes

Quando são utilizados métodos construtores da classe, estes devem sempre retornar tipo de 'instancetype' e nunca 'id'. Isso garante que o compilador infere corretamente o tipo de resultado.

```objc
@interface Airplane
+ (instancetype)airplaneWithType:(RWTAirplaneType)type;
@end
```

## Funções CGRect

Ao acessar o `x`,` y`, `width`, ou`hight`de um `CGRect` , sempre use o [`CGGeometry` functions](http://developer.apple.com/library/ios/#documentation/graphicsimaging/reference/CGGeometry/Reference/reference.html) em vez de acesso direto a struct. A partir da Apple `referência CGGeometry`:

> Todas as funções descritas nesta referência que ter estruturas de dados CGRect como entradas implicitamente padronizar esses retângulos antes de calcular os seus resultados. Por esta razão, as aplicações devem evitar directamente a leitura e escrita dos dados armazenados na estrutura de dados CGRect. Em vez disso, use as funções descritas aqui para manipular retângulos e para recuperar as suas características.

**Exemplo correto:**

```objc
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
CGRect frame = CGRectMake(0.0, 0.0, width, height);
```

**Inadequado:**

```objc
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
CGRect frame = (CGRect){ .origin = CGPointZero, .size = frame.size };
```


## Singletons

Singleton objects should use a thread-safe pattern for creating their shared instance.

```objc
+ (instancetype)sharedInstance {
  static id sharedInstance = nil;

  static dispatch_once_t onceToken;
  dispatch_once(&onceToken, ^{
    sharedInstance = [[self alloc] init];
  });

  return sharedInstance;
}
```

## TableView

Utilizar o próprio nome da classe para definir os identificadores

```objc
[tableview registerClass:[MyCell class] forCellReuseIdentifier:NSStringFromClass([MyCell class])];
```


```objc
[self.tableView registerNib:[UINib nibWithNibName:NSStringFromClass([GameCell class]) bundle:[NSBundle mainBundle]]
     forCellReuseIdentifier:NSStringFromClass([GameCell class])];
```

```objc
GameCell *cell = [tableView dequeueReusableCellWithIdentifier:NSStringFromClass([GameCell class]) forIndexPath:indexPath];
```