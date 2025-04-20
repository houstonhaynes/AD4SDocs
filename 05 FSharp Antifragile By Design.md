# F#: Antifragile By Design From Day One

## Introduction: The Language That Thrives on Change

In the ever evolving landscape of programming languages, most systems strive merely for robustness, the ability to withstand stress without breaking. F#, however, has demonstrated a rarer quality: antifragility, the capacity to not just survive volatility but to actively improve from it. From its inception two decades ago as "OCaml for .NET" to its current position spanning web development, data science, and native compilation, F# exemplifies how thoughtful language design can create systems that gain from disorder rather than bolting on ill-fitted adaptations.

This article examines F#'s journey through the lens of antifragile design principles, exploring how its core design decisions, evolutionary path, and growing ecosystem embody the characteristics that allow systems to thrive amid uncertainty and change. Central to this story is F#'s remarkable influence on other languages, a manifestation of "ersatz optionality" where languages like C#, JavaScript, and even Swift and Rust have looked to F# as a source of well-principled features they could adapt to their own paradigms.

## Origins: A Functional Foundation Built for Adaptation

F# began its life in 2002 when Don Syme at Microsoft Research Cambridge set out to bring functional programming principles to the .NET ecosystem. Rather than creating an entirely new language, Syme made the strategic decision to base F# on OCaml, an established functional language with proven foundations in type theory.

This decision embodied the first principle of antifragile design: building on well established foundations while maintaining optionality for novel exploration. By adopting OCaml's syntax and type system, F# inherited decades of research in programming language theory. And by integrating with .NET, it gained a new landscape of opportunities which led to a vast ecosystem of libraries and tools.

The hybrid nature of F# was revolutionary. As a functional-first language with full access to an object-oriented ecosystem, F# occupied a unique position that allowed it to bridge paradigms rather than forcing developers to choose between them. This boundary-spanning quality would become a defining feature of F#'s antifragility.

## Don Syme's Innovations: Generics and Beyond

Don Syme, F#'s creator, developed several foundational innovations that would prove transformative far beyond F#'s direct user base. These innovations exemplify the antifragile principle of "skin in the game", theoretical knowledge applied to practical problems with real consequences:

### Generics: Cross-Language Type Safety

One of F#'s most significant contributions to the programming landscape came before the language itself was fully formed. In 2001, Don Syme led the design and implementation of generics for .NET, which would fundamentally transform the platform's type system and exhibit influence throughout modern software language design. His paper "Design and Implementation of Generics for the .NET Common Language Runtime" (with Andrew Kennedy) laid the foundation for bringing parametric polymorphism to a mainstream commercial platform in a way that previous attempts had not achieved.

The implementation of generics in .NET was revolutionary because, unlike Java's approach of type erasure, it maintained full type information at runtime through reification. This design choice created a more robust system that could enforce type safety across language boundaries, a critical feature for a multilingual platform like .NET.

The influence of this work extended far beyond Microsoft's ecosystem. Java eventually adopted similar concepts in its generics implementation, and modern languages like Kotlin and Swift incorporated lessons from .NET's approach. This pattern of F# innovations influencing broader language development would become a recurring theme.

### Asynchronous Programming: A New Programming Model

Perhaps Don Syme's most visionary contribution was his work on asynchronous programming models. In 2007, years before async/await became ubiquitous, Syme introduced async workflows in F#, a revolutionary approach to managing concurrency through computational expressions.

```fsharp
// F# async workflows (introduced in 2007)
let fetchAndProcessData url = async {
    let! data = httpClient.GetStringAsync(url) |> Async.AwaitTask
    let processed = processData data
    return processed
}

// Process multiple URLs concurrently
let processUrls urls =
    urls
    |> Seq.map fetchAndProcessData
    |> Async.Parallel
    |> Async.RunSynchronously
```

This model directly inspired:

- **C# async/await** (2012): The C# team explicitly acknowledged F#'s influence on their design
- **JavaScript**: The `async/await` pattern added to ECMAScript 2017
- **Python**: Added similar syntax in Python 3.5 (PEP 492)
- **Rust**: The `async/.await` system
- **Kotlin**: Coroutines and structured concurrency
- **Swift**: Async/await implementation

The pattern's adoption across such diverse languages demonstrates its fundamental insight: code should be structured in a way that aligns with human intuition about sequential and parallel execution. Martin Odersky, creator of Scala, noted in private correspondence with Syme: "I enjoyed a lot discussing with you at the WG 2.8. I have been thinking how to do active patterns in Scala."[^1]

This approach exemplifies the antifragile property of being "long gamma", creating outsized positive impacts from positive changes in the environment. As computing increasingly moved toward concurrent and distributed models, F#'s async approach proved prescient, positioning the language's continued influence to inspire rather than merely survive this paradigm shift.

## Extensible by Design: The Secret of F#'s Adaptability

F#'s most underappreciated quality may be its inherent extensibility, not just as an implementation detail, but as a core design principle. Several language features demonstrate this commitment to extensibility:

### Type Providers: Compile-Time Metaprogramming

Type providers, introduced in F# 3.0 (2012), represent a fundamental innovation in how programming languages can interact with external data sources. Unlike traditional code generation approaches, type providers create types on demand during compilation, enabling seamless integration with diverse data sources without requiring explicit mappings or code generation steps.

```fsharp
// Using a type provider for CSV data
type StockData = CsvProvider<"stocks.csv">
let data = StockData.Load("stocks.csv")

// Compiler knows the structure
for row in data.Rows do
    printfn "%s: %.2f" row.Symbol row.Price
```

This feature embodies the antifragile property of optionality, the ability to exploit favorable opportunities without commitment. Type providers allow F# programs to adapt to changing data schemas without requiring code changes, creating a system that can respond to data evolution with minimal friction.

This innovation influenced:
- **TypeScript**: Declaration files serve a similar purpose
- **Scala**: Implicit macros and later Scala 3's metaprogramming
- **Haxe**: Macro system for type generation
- **C#**: The source generator system introduced in .NET 5

Luke Hoban, one of TypeScript's original developers, worked on F# 2.0 before moving to the TypeScript team, bringing with him insights from F#'s approach to type safety and inference. As he noted in a 2017 presentation: "The extent and nature of this influence is a matter of debate, but it is my opinion that TypeScript is firmly based on positive experience of advanced type checking and inference in the context of F#."[^2]

### Computation Expressions: Domain-Specific Sublanguages

F#'s computation expressions provide a framework for creating domain-specific sublanguages within F# itself. This feature powers async workflows, query expressions, and numerous other patterns, allowing developers to extend the language for specific domains without requiring changes to the compiler.

```fsharp
// Creating a custom computation expression for validation
type ValidationBuilder() =
    member _.Bind(result, f) =
        match result with
       <br>Ok value -> f value
       <br>Error e -> Error e
    member _.Return(value) = Ok value

let validate = ValidationBuilder()

// Using the custom computation expression
let validateUser input = validate {
    let! name = validateName input.Name
    let! email = validateEmail input.Email
    let! age = validateAge input.Age
    return { Name = name; Email = email; Age = age }
}
```

This extensibility mechanism represents the antifragile principle of convex tinkering, creating small, controlled experiments with limited downside but potentially significant upside. 

### Units of Measure: Zero-Cost Type Safety

Units of measure, introduced in F# 2.0, provide compile-time checking of physical units while generating the same efficient code as untyped computations. This feature prevents common errors such as confusing meters with feet or adding velocities to accelerations.

```fsharp
[<Measure>] type m    // meters
[<Measure>] type s    // seconds
[<Measure>] type kg   // kilograms
[<Measure>] type N = kg m / s^2  // newtons (derived unit)

// Use with type safety
let gravity = 9.81<m/s^2>
let mass = 10.0<kg>
let force = mass * gravity  // Type: float<N>

// This would cause a compile-time error:
// let error = force + mass
```

This feature demonstrates how F# embodies the barbell strategy of antifragile design, combining extreme safety (static typing of physical dimensions) with high performance (zero runtime overhead). The compiler enforces correctness, but the generated code is as efficient as if no checks were performed.

This innovation has influenced:

- **Rust**: Libraries like `uom` and their discussions of first-class support
- **Swift**: Measurement types in Foundation
- **C++**: Dimensional analysis libraries
- **Python**: Libraries like Pint

## The Fable Phenomenon: Creating a Safe Way to Develop for the Web

F#'s antifragility became even more apparent with the emergence of Fable, a community-led compiler that transpiles F# to JavaScript. Created by Alfonso Garcia-Caro in 2016, Fable demonstrated how F#'s clean semantic model could be targeted to environments far beyond its original .NET home.

```fsharp
// F# code for a web application using Fable
open Fable.React
open Fable.React.Props

let counter() =
    let (count, setCount) = React.useState(0)
    
    div [] [
        h1 [] [str (sprintf "Count: %d" count)]
        button [
            OnClick (fun _ -> setCount(count + 1))
        ] [str "Increment"]
    ]
```

Fable's success illustrates several antifragile properties:

1. **Optionality**: F# developers gained the ability to target browser environments without switching languages
2. **Barbell Strategy**: Combining the safety of F#'s type system with the reach of the JavaScript ecosystem
3. **Skin in the Game**: Community-driven development ensured that Fable addressed real-world problems

Perhaps most importantly, Fable demonstrated that F#'s fundamental design was platform-agnostic, its value proposition wasn't tied to .NET, but to its core principles of functional-first programming, strong type safety, and pragmatic design.

## F# Through The Years

Perhaps the most compelling evidence of F#'s antifragile nature is its outsized influence on other programming languages relative to its market share. This timeline traces how F#'s innovations have propagated throughout the industry, demonstrating its role as a catalyst for broader language evolution:

### 2001-2005: The Foundation Years

- Don Syme develops .NET generics, which become fundamental to C# 2.0
- Early F# designs influence C# 3.0 features including LINQ

### 2007-2010: The Async Revolution

- F# introduces async workflows (2007)
- The Reactive Extensions (Rx) project is directly influenced by F#'s event handling
- C# team begins discussion of async/await based on F#'s model

### 2010-2015: Functional Goes Mainstream

- C# 5.0 adds async/await (2012), explicitly influenced by F#
- F# type providers demonstrate a new approach to type-safe data access
- Swift launches (2014) with numerous F#-influenced features
- TypeScript development accelerates, influenced by F# type system concepts

### 2015-2020: The Pattern Matching Era

- C# 7.0 adds pattern matching and tuples (2017), directly influenced by F#
- C# 8.0 enhances pattern matching further (2019)
- JavaScript proposes pattern matching with F# influence
- Rust 1.0 launches with features influenced by ML-family languages including F#

### 2020-Present: Convergent Evolution

- C# 9.0 adds non-null as default, following F#'s lead
- Most major languages now include async/await patterns
- Pipeline operators continue to spread to more languages
- Active patterns and computational expressions influence more language designs

## The Fidelity Framework: Beyond Runtime Boundaries

The most recent evolution in F#'s antifragile journey is the Fidelity Framework, which takes F#'s adaptability to unprecedented levels. While Fable brought F# to the browser, Fidelity takes F# "to the metal," enabling direct compilation to native code across the entire computing spectrum, from microcontrollers to cloud servers. The adaptation of F# to MLIR through a straightforward translation layer is a testament to both systems carrying their own deep antifragile principals into real world utility.

### Transcending Runtime Limitations

Fidelity's design eliminates traditional barriers between high-level languages and hardware:

```fsharp
// Directly binding to hardware registers on an ARM microcontroller
[<Measure>] type reg32  // Register address space
type GPIOPort = 
    { BASE_ADDR: int<reg32>
      MODER: int<reg32>     // Mode register
      ODR: int<reg32>       // Output data register
      IDR: int<reg32> }     // Input data register

// Direct memory-mapped hardware access without RTOS involvement
let toggleLED (port: GPIOPort) (pin: int) =
    // Read current value directly from hardware register
    let current = !*(port.ODR |> NativePtr.ofNativeInt)
    // Toggle pin
    let newValue = current ^^^ (1 <<< pin)
    // Write directly to hardware register
    !*(port.ODR |> NativePtr.ofNativeInt) <- newValue
```

This approach embodies several antifragile design principles:

### Optionality Through Multi-Target Compilation

The Fidelity Framework maximizes optionality by enabling a single F# codebase to target virtually any computing environment:

```fsharp
// Configure for embedded target
let embeddedConfig = 
    PlatformConfig.compose [
        withPlatform PlatformType.Embedded
        withMemoryModel MemoryModelType.Constrained
        withVectorCapabilities VectorCapabilities.Minimal
    ] PlatformConfig.base'

// Configure for server target
let serverConfig = 
    PlatformConfig.compose [
        withPlatform PlatformType.Server
        withMemoryModel MemoryModelType.Abundant
        withVectorCapabilities VectorCapabilities.Advanced
    ] PlatformConfig.base'
```

This creates unprecedented adaptability, the same F# code can run on devices spanning the entire computing spectrum, from tiny microcontrollers with kilobytes of memory to massive server clusters with terabytes of RAM.

### Barbell Strategy: Type Safety with Bare Metal Performance

The Fidelity Framework implements a perfect barbell strategy that combines F#'s strong type safety with direct hardware access:

```fsharp
// High-level F# code with strong type safety
[<Measure>] type celsius
[<Measure>] type fahrenheit

let convertCtoF (temp: float<celsius>) : float<fahrenheit> =
    temp * 1.8<fahrenheit/celsius> + 32.0<fahrenheit>

// Direct compilation to hardware-specific instructions
// with no runtime overhead
```

This approach provides both safety and performance without compromise, the type checking occurs at compile time, while the generated code is as efficient as hand-written C.

### "Let It Fail" Architecture Inspired by Erlang

Taking inspiration from Erlang's robust "let it fail" actor model, Fidelity enables resilient systems through isolation and failure detection:

```fsharp
// Supervisor pattern for hardware component management
type ComponentResult<'T> = 
   <br>Success of 'T 
   <br>Failure of string

// Supervisor that monitors hardware components
let supervisorLoop components =
    let rec loop runningComponents =
        match waitForNextEvent() with
       <br>ComponentFailure(id, reason) ->
            // Isolate failure to just this component
            let newComponents = 
                Map.change id (fun comp -> 
                    Some { comp with 
                             Status = Restarting
                             RestartCount = comp.RestartCount + 1 }) 
                    runningComponents
                    
            // Restart if under threshold, otherwise alert
            if getComponent(id, newComponents).RestartCount < maxRestarts
            then restartComponent(id)
            else alertSystemFailure(id, reason)
            
            loop newComponents
       <br>_ -> loop runningComponents
        
    loop initialComponents
```

This approach enables F# code to run with extreme efficiency in environments previously exclusive to languages like C, while maintaining much stronger safety guarantees and fault tolerance.

### BAREWire: Advanced Type-Safe Communication Protocol

A critical component of this system is BAREWire, SpeakEZ's (the primary architects of the Fidelity Framework) patent-pending implementation of the BARE protocol that includes zero-copy memory management as well as fully type-safe inter-process and network communications:

```fsharp
// Define memory layout matching hardware requirements
let modelWeightLayout = {
    Alignment = 8
    Fields = [
        { Name = "binary"; Type = BitArray; Offset = 0 }
        { Name = "scale"; Type = Float; Offset = BitArray.byteSize }
    ]
    Size = BitArray.byteSize + 4
}

// Create model buffer that can be directly accessed by hardware
let createModelWeightBuffer count =
    AlignedBuffer<BitNetWeight>.Create(count, modelWeightLayout, true)
    
// Process model data with zero copying
let processModelWeights (buffer: AlignedBuffer<BitNetWeight>) =
    // Direct access to memory shared with hardware
    for i = 0 to buffer.Length - 1 do
        let weight = buffer.[i]
        
        // Specialized hardware operations on binary weights
        match currentPlatform with
       <br>ASIC -> ASICOperations.xnorPopcount(weight.binary)
       <br>GPU -> GPUOperations.parallelPopcount(weight.binary)
       <br>_ -> CPUOperations.vectorizedPopcount(weight.binary)
```

BAREWire enables F# code to directly manipulate memory in ways that are optimized for each hardware target, eliminating the performance penalties typically associated with managed languages in AI workloads. It completely eliminates "runtime bloat" and allows marshaling of communication and memory mapping between CPU and GPU resources at the speed of the systems memory bus.

## Advanced BitNet Deployments: Antifragility for AI in 2025 and Beyond

The latest evolution in F#'s antifragile journey is SpeakEZ's continuing research - design elements that continue to yield unexpected benefits as computing paradigms shift. SpeakEZ's groundbreaking work with the Fidelity Framework demonstrates how F#'s type system, particularly its unique Units of Measure feature, has enabled a revolutionary approach to deploying efficient AI models across the entire computing spectrum.

### Multi-Target BitNet Deployments

BitNet models represent a significant advancement in AI efficiency, using binary or ternary weights (-1, 0, +1) with scaling factors to create neural networks that are 32x smaller than traditional models. F#'s type system has proven uniquely suited to implement these models with both safety and performance:

```fsharp
// Define unit types for tensor safety
module TensorTypes =
    // Unit types for tensor value ranges
    type [<Measure>] Binary      // For tensors with only -1.0 or 1.0 values
    type [<Measure>] Scale       // For positive scaling factors
    type [<Measure>] FullPrecision // For standard floating-point tensors
    
    // Unit types for tensor dimensions
    type [<Measure>] VocabDim     // Vocabulary dimension
    type [<Measure>] HiddenDim    // Hidden layer dimension
    
    // Type aliases for better readability and safety
    type BinaryTensor = Tensor<Binary>
    type ScaleTensor = Tensor<Scale>
    type BitNetWeight = BinaryTensor * ScaleTensor

// Module for enforcing binary value constraints
module BinaryConstraints =
    // Private constructor - can't be called directly from outside
    let private tagUnsafe (t: Tensor) : BinaryTensor = UMX.tag<Binary> t
    
    // Validate that a tensor contains only -1.0 or 1.0 values
    let validateBinary (t: Tensor) : bool =
        let squared = dsharp.pow(t, 2)
        let allOnes = dsharp.eq(squared, dsharp.tensor(1.0f))
        dsharp.all(allOnes).ToBoolean()
    
    // Public smart constructor with validation
    let createChecked (t: Tensor) : BinaryTensor option =
        if validateBinary t then
            Some (tagUnsafe t)
        else
            None
```

This dual-layered type safety approach uses F#'s Units of Measure to enforce both dimensional constraints and binary value restrictions throughout the model lifecycle. The result is a system that can guarantee correctness while maintaining the performance benefits of binary neural networks.

### Cross-Target Deployment with One Codebase

What truly demonstrates F#'s antifragility is the ability to deploy these BitNet models across the entire computing spectrum, from CPUs to GPUs to specialized ASICs, using a single codebase:

```fsharp
// CPU resource configuration
let cpuConfig = 
    PlatformConfig.compose 
        [withPlatform PlatformType.CPU;
         withMemoryModel MemoryModelType.Constrained;
         withBitPrecision PrecisionType.Ternary;
         withVectorization VectorizationType.SIMD]
        PlatformConfig.base'

// GPU resource configuration
let gpuConfig = 
    PlatformConfig.compose 
        [withPlatform PlatformType.GPU;
         withMemoryModel MemoryModelType.Abundant;
         withBitPrecision PrecisionType.Ternary;
         withSharedMemory true]
        PlatformConfig.base'

// ASIC resource configuration
let asicConfig = 
    PlatformConfig.compose 
        [withPlatform PlatformType.ASIC;
         withBitPrecision PrecisionType.Binary;
         withHardwareXNOR true;
         withPopCountHardware true]
        PlatformConfig.base'
```

This future state would enable developers to compile and deploy substantially similar F# BitNet code to radically different hardware targets without changing the core logic. While current work is adapting to existing hybrid approaches, SpeakEZ's work in this area focuses on a strata of platform code that would automatically adapt memory management and code optimization strategies based on a declarative target platform configuration. This could herald a new era, creating previously unexpressed degrees of freedom for deploying robust heterogenous workloads, and laying basis for more groundbreaking efficiency as the new AI landscape continues to take shape.

What's crucial to understand is that while Fidelity takes a practical hybrid approach by leveraging existing technologies like .NET tooling and platform-specific compilers, this future state of true hardware independence is only achievable because of F#'s fundamental design principles. The language's layered separation of concerns, from its type system to its effect management to its computation expressions, creates what could be called "progressive optionality." Each layer maintains independence while preserving the ability to specialize at later stages.

Consider how this works: F#'s type system enforces correctness independent of execution model; its immutability-by-default ensures reasoning about code remains valid across platforms; and its computation expressions provide a clean separation between what computation is performed and how it executes. Unlike languages where runtime assumptions are baked into the core design, F# was built with this layered abstraction from day one. This is why Fidelity can transform the same high-level F# code into radically different execution models, from garbage-collected runtime to bare-metal execution to specialized AI hardware, without requiring developers to choose a new language or unfamiliar technology stack. The optionality is preserved throughout the compilation pipeline, a quality that cannot be retrofitted onto languages lacking these foundational principles.

### Dynamic Orchestration Across Hardware Boundaries

The ultimate demonstration of F#'s antifragility is in SpeakEZ's design for a BitNet Orchestration system, which dynamically distributes AI workloads across heterogeneous hardware based on resource availability and task complexity:

```fsharp
// BitNet Orchestration system for cross-hardware deployment
type BitNetOrchestrator(configs: Map<PlatformType, PlatformConfig>) =
    // Create actor system for model coordination
    let system = Actor.createSystem "BitNetOrchestration"
    
    // Create router model (always on CPU for reliability)
    let router = createModelActor ModelType.Router configs.[PlatformType.CPU]
    
    // Create specialists on various hardware targets
    let specialists = 
        [
            ModelType.Specialist Domain.TextProcessing, PlatformType.CPU;
            ModelType.Specialist Domain.ImageAnalysis, PlatformType.GPU;
            ModelType.Specialist Domain.AudioProcessing, PlatformType.GPU;
            ModelType.Specialist Domain.BinaryClassification, PlatformType.ASIC
        ]
        |> List.map (fun (modelType, platform) -> 
            modelType, createModelActor modelType configs.[platform])
        |> Map.ofList
    
    // Process input through the orchestration system
    member this.Process(input: Input) = async {
        // First route the input to determine which specialist to use
        let! routingResult = router.Ask(Process(input, None))
        
        match routingResult with
       <br>Success domain ->
            // Forward to appropriate specialist based on routing
            return! specialists.[ModelType.Specialist domain].Ask(Process(input, None))
       <br>Failure error ->
            // Handle routing failure
            return Failure $"Routing failed: {error}"
    }
```

While there's always a system-dependent demand for knowledge of a given device or platform's capability, this orchestration system will enable flexible segmentation and deployment of AI workloads across the entire computing spectrum, from CPUs to GPUs and even to specialized ASICs, all while maintaining the type safety and functional programming benefits of F#.

## Conclusion: F# as the Nexus of Antifragile Design

As we reflect on F#'s remarkable journey, its enterprise-grade reliability, firmly established through its deep integration with the mature .NET ecosystem, stands as a testament to its practical foundations. Yet F# has never been content to rest on these foundations alone. The Fable compiler demonstrated that F# could tackle modern web development with equal aplomb, bringing its powerful type system and functional elegance to JavaScript environments and beyond. Now, the Fidelity Framework emerges as the third pillar in this triumvirate, borrowing strengths from both previous approaches while forging bold new territory for the AI-driven landscape of tomorrow. What's truly extraordinary is that Don Syme's early design decisions, made over two decades ago in a Microsoft Research lab, have generated what can only be described as "gravitational waves" that continue to ripple through our technological universe, influencing languages, frameworks, and paradigms far beyond what anyone could have predicted. These careful, principled choices have created not just a language, but a movement that continues to expand its reach and relevance with each technological shift.

F# stands as a remarkable example of antifragile design in programming languages, not merely surviving but thriving amid two decades of rapid technological change. From its origins as "OCaml for .NET" to its current position spanning multiple compilation targets and computing environments, F# has demonstrated the key qualities of antifragile systems:

1. **Optionality**: Multiple compilation targets and deployment choices
2. **Barbell Strategy**: Combining high-level safety with low-level performance
3. **Via Negativa**: Simplifying through composition and principled design
4. **Skin in the Game**: Community-driven innovation addressing real-world needs
5. **Convex Tinkering**: Controlled experimentation showing minimal risk for outsized reward

What makes F# particularly notable is that these antifragile qualities weren't retrofitted, they were present from day one in its fundamental design. Don Syme's vision of a functional-first language that could operate seamlessly in a predominantly object-oriented ecosystem established a foundation of adaptability that has enabled F# to evolve in ways that would have been difficult to predict at its inception.

This represents the ultimate fulfillment of Antifragile Design For Systems, not just surviving technological shifts but actively thriving as new computational paradigms emerge. F#'s deep foundations have created a system uniquely positioned for the future of computing, where volatility becomes advantage and disruption becomes opportunity, transforming each new challenge into a pathway for greater success.

## References

[^1]: Syme, D. (2020). The Early History of F#. Proceedings of the ACM on Programming Languages, Vol. 4, No. HOPL, Article 75. p. 75:30. https://fsharp.org/history/hopl-final/hopl-fsharp.pdf

[^2]: Syme, D. (2020). The Early History of F#. p. 75:49-75:50. https://fsharp.org/history/hopl-final/hopl-fsharp.pdf

[^3]: Syme, D. (2020). The Early History of F#. p. 75:50. https://fsharp.org/history/hopl-final/hopl-fsharp.pdf
