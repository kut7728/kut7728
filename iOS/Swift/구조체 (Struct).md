---
설명: OOP의 캡슐화 방법중 하나, Class와 유사한 녀석
---
> [!important] OOP의 캡슐화 방법중 하나, Class와 유사한 녀석

- 목차
    - [[#Struct 선언]]
    - [[#Instance 선언]]
    - [[#init 메소드 초기화]]
    - [[#Method]]
        - [[#Structure Method]]
        - [[#Mutating Method]]
    - [[#Final Practice]]

  

> Class와의 공통점과 차이점

Struct

- 값 타입 - 인스턴스 복사시 복사본을 생성
- 상속, 하위클래스 미지원

Class

- 참조 타입 - 인스턴스 복사시 원본 인스턴스를 참조하는 참조체 생성

  

  

  

### Struct 선언

```Swift
struct Dog {
  var age: Int
  var isGood: Bool
  
  var test = "like this"
}
```

- 데이터 타입의 이름은 첫문자가 대문자
- 괄호 속에는 properties 와 method 가 선언됨
- 디폴트 값을 미리 정해놓을 수 있다.

  

### Instance 선언

```Swift
var eloise = Dog(age: 3)

print(eloise.age)
// 3

eloise.age = 12
print(eloise.age)
// 12
```

- 인스턴스의 properties 참조하려면 `[인스턴스이름].[property이름]`

  

### init 메소드 초기화

```Swift
struct Book {
	var title: String
	var pages: Int
	
	init (title: String, pages: Int) {
		self.title = title
		self.pages = pages
	}
}
---
var littleMermaid = Book(title: "The little mermaid", pages: 400)
```

- struct 내부에 init 메소드를 넣고 self를 통해 자기자신을 참조하면서 argument 로 초기화
- **사실 init 없어도 argument 로 초기화 가능, 하지만 init 쓰는게 동료의 시인성에 좋음**

  

## Method

### Structure Method

```Swift
struct Band {
  var genre: String
  var members: Int
  var isActive: Bool
  
  init(genre: String, members: Int, isActive: Bool) {
    self.genre = genre
    self.members = members
    self.isActive = isActive
  }

  func pumpUpCrowd() -> String {
    if self.isActive == true {
      return "Are you ready to ROCK?"
    } else {
      return "..."
    }
  }
}

var fooFighters = Band(genre: "rock", members: 6, isActive: true)
print(fooFighters.pumpUpCrowd())
```

  

### Mutating Method

```Swift
struct Dog {
  var age : Int
  var isGood : Bool

  init(age: Int, isGood: Bool) {
    self.age = age
    self.isGood = isGood
  }

  // birthday() is a mutating method:
  mutating func birthday() -> Int {
    print("Best doggy")
    self.age += 1
    return self.age
  }
}
```

- instance의 property를 변경시킬 수 있는 메소드
- 만약 mutating 키워드 없이 일반 메소드로 같은 코드를 작성하면
    
    → self 는 mutable하지 않다면서 mutating 키워드를 통해 mutable하게 바꾸라고 뜸
    

  

## Final Practice

```Swift
struct Exercise {
  var name: String
  var muscleGroups: [String]
  var reps: Int
  var sets: Int
  var totalReps: Int

  init (name: String, muscleGroups: [String], reps: Int, sets: Int) {
    self.name = name
    self.muscleGroups = muscleGroups
    self.reps = reps
    self.sets = sets
    self.totalReps = reps * sets
  }
}

var pushUp = Exercise(name: "Push up", muscleGroups: ["Triceps", "Chest", "Shoulders"], reps: 10, sets: 3)

var crossFit = Exercise(name: "crossFit", muscleGroups: ["Triceps", "Chest", "Shoulders"], reps: 20, sets: 4)

var sLL = Exercise(name: "sLL", muscleGroups: ["Triceps", "Chest", "Shoulders"], reps: 30, sets: 2)

var dumbBell = Exercise(name: "dumbBell", muscleGroups: ["Triceps", "Chest", "Shoulders"], reps: 10, sets: 4)

// print(pushUp)

struct Regimen {
  var dayOfWeek: String
  var exercises: [Exercise]

  init (dayOfWeek: String, exercises: [Exercise]) {
    self.dayOfWeek = dayOfWeek
    self.exercises = exercises
  }

  func printExercisePlan() -> Void {
    print("Today is \(self.dayOfWeek) and the plan is to: ")
    for exercise in self.exercises {
      print("Do \(exercise.sets) sets of \(exercise.reps) \(exercise.name)s")

      print("That's a total of \(exercise.totalReps) \(exercise.name).")
    }
  }

  mutating func addExercise(of: [Exercise]) -> Void {
    for i in of {
      self.exercises.append(i)
    }
  }
}

var mondayRegimen = Regimen(dayOfWeek: "Monday", exercises: [pushUp, sLL, dumbBell])

var wednesdayRegimen = Regimen(dayOfWeek: "Wednesday", exercises: [crossFit, sLL, dumbBell])

var thursdayRegimen = Regimen(dayOfWeek: "Thursday", exercises: [])

// print(mondayRegimen)
// print("")
// print(mondayRegimen.printExercisePlan())
// print(wednesdayRegimen.printExercisePlan())
// wednesdayRegimen.addExercise(of: [pushUp])
// print(wednesdayRegimen.printExercisePlan())

print(thursdayRegimen.printExercisePlan())
thursdayRegimen.addExercise(of: [pushUp, sLL, dumbBell, crossFit])
print(thursdayRegimen.printExercisePlan())


```