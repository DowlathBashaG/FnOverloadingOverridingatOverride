# FnOverloadingOverridingatOverride

Function overriding examples and answers and Function overloading and answers from Java

📘 1. Function Overloading (Compile-time Polymorphism)

			➡️ What is it?
			Same method name, but different parameters (type/number/order).

			Happens inside the same class.

			Resolved at compile-time.

✨ Example of Overloading:

			public class OverloadingExample {

				void show() {
					System.out.println("No-arg method");
				}

				void show(int a) {
					System.out.println("Method with int: " + a);
				}

				void show(String s) {
					System.out.println("Method with String: " + s);
				}

				void show(int a, String s) {
					System.out.println("Method with int and String: " + a + ", " + s);
				}

				public static void main(String[] args) {
					OverloadingExample obj = new OverloadingExample();
					obj.show();                 // No-arg method
					obj.show(10);                // Method with int
					obj.show("Hello");           // Method with String
					obj.show(20, "World");       // Method with int and String
				}
			}
🧠 Output:

			No-arg method
			Method with int: 10
			Method with String: Hello
			Method with int and String: 20, World
			
💡 Key Points of Overloading:

			Methods must differ by parameters.

			Return type can be same or different, but it does NOT matter in overloading.

			Compiler chooses based on best match.

📗 2. Function Overriding (Run-time Polymorphism)

			➡️ What is it?
			Same method name, same parameters in parent and child class.

			Achieved by inheritance (subclass).

			Resolved at runtime.

✨ Example of Overriding:

			class Parent {
				void display() {
					System.out.println("Parent display()");
				}
			}

			class Child extends Parent {
				@Override
				void display() {
					System.out.println("Child display()");
				}
			}

			public class OverridingExample {
				public static void main(String[] args) {
					Parent p = new Parent();
					p.display();           // Parent display()

					Child c = new Child();
					c.display();           // Child display()

					Parent ref = new Child();
					ref.display();         // Child display() -> Runtime polymorphism
				}
			}
🧠 Output:

			Parent display()
			Child display()
			Child display()
			
💡 Key Points of Overriding:

			Method name, parameters must be same.

			Access modifier can be more visible (e.g., protected → public).

			Return type should be same or covariant (subtype allowed).

			Only instance methods can be overridden (not static methods).

Use @Override annotation (good practice).

			📚 Overloading vs Overriding in short

			Feature				Overloading			Overriding
			
			Where				Same class			Parent-Child classes
			Parameters			Must be different	Must be same
			Return 	Type		        Can be different	Must be same/covariant
			Timing				Compile-time		Runtime
			Polymorphism Type	        StaticPolymorphism	Dynamic Polymorphism
			
🎯 Example: Both Overloading + Overriding Together

			class Animal {
				void sound() {
					System.out.println("Animal makes a sound");
				}

				void sound(int times) {
					System.out.println("Animal makes sound " + times + " times");
				}
			}

			class Dog extends Animal {
				@Override
				void sound() {
					System.out.println("Dog barks");
				}

				void sound(String barkType) {
					System.out.println("Dog barks like: " + barkType);
				}
			}

			public class BothExample {
				public static void main(String[] args) {
					Dog dog = new Dog();
					dog.sound();                 // Overridden version -> Dog barks
					dog.sound(3);                 // Overloaded version -> Animal makes sound 3 times
					dog.sound("Loudly");          // Overloaded in Dog -> Dog barks like: Loudly

					Animal animal = new Dog();
					animal.sound();               // Runtime polymorphism -> Dog barks
				}
			}
🧠 Output:

			Dog barks
			Animal makes sound 3 times
			Dog barks like: Loudly
			Dog barks
			
🛑 Common Mistakes Interviewers Check:

			Overloading can't be done only by changing return type.

			Static methods cannot be overridden (they can be hidden).

			Private methods cannot be overridden.

			Constructors cannot be overridden.



Higher Precedence Order .... 


In the function overloading show(Object o) method is there, in this case ,show(String s) ....when i call show(null) which one will call is it will it through the exception?

❓ Scenario you are asking:
Suppose you have overloaded methods like:

			public class OverloadingTest {

				void show(Object o) {
					System.out.println("Object method called");
				}

				void show(String s) {
					System.out.println("String method called");
				}

				public static void main(String[] args) {
					OverloadingTest test = new OverloadingTest();
					test.show(null);
				}
			}
			
🎯 What Happens When You Call show(null)?

			✅ Java will always choose the most specific method in case of ambiguity.

			String is more specific than Object (because String extends Object).

			So show(String s) will be called.

🔥 Thus, output will be:

			String method called
🧠 Why?

			Because in method overloading, Java compiler tries to pick the most specific match available at compile time.

			If multiple methods are applicable, Java will prefer child class types (String) over parent class types (Object).

			String → child

			Object → parent

			And since String is a subclass of Object, show(String s) is more specific than show(Object o).

⚡ Important: What if two methods are at the same specificity level?

			If the compiler cannot decide (for example, if two classes are sibling classes), then compile-time error occurs (ambiguity!).

Example:

			void show(StringBuffer sb) { }
			
			void show(StringBuilder sb) { }
			
			If you call show(null), then compile error happens because both StringBuffer and StringBuilder are at the same level — siblings, not parent/child.

⚡ Final Conclusion:

			Situation	Behavior
			Object and String	String version called
			Two sibling classes (like StringBuffer, StringBuilder)	Compile-time Error
			✅ Short Answer:
			❝ show(String s) will be called when you call show(null). It will NOT throw any exception. ❞

✨ Bonus Small Diagram:

Object
			↳ String   (more specific)
			When passing null, Java prefers String over Object.

			when will get ambiquity error or expcetion will come 


❓ When do you get AMBIGUITY in Function Overloading?

			👉 You get a compile-time error (not runtime exception) when the compiler cannot figure out which overloaded method to call because multiple methods are equally matching, and none is more specific than the others.

📕 Typical case:

			If two (or more) overloaded methods could be matched equally for the same call (especially with null),

			and they do not have a clear parent-child relationship (they are siblings),

			Java gets confused and gives a compile-time ambiguity error ❗.

⚡ Example of Ambiguity Error:

			public class AmbiguityExample {

				void show(StringBuffer sb) {
					System.out.println("StringBuffer method called");
				}

				void show(StringBuilder sb) {
					System.out.println("StringBuilder method called");
				}

				public static void main(String[] args) {
					AmbiguityExample obj = new AmbiguityExample();
					obj.show(null); // ❗ Compiler Error: reference to show is ambiguous
				}
			}
			
🧠 Why Error?

			StringBuffer and StringBuilder are two different classes, both extend Object, but are not related to each other (they are siblings).

			When you pass null, compiler cannot decide:
			➔ Should it go to show(StringBuffer) OR show(StringBuilder)?

➡ Result:

			Error: reference to show is ambiguous
			✅ So you get a compile-time error (NOT an exception)!

📚 Summary Table

			Situation	Result
			Parent vs Child	Child method is called
			Two sibling classes	Compile-time Ambiguity Error
			No matching method	Compile-time Error (method not found)
			🚫 You will NOT get a Runtime Exception in Overloading!
			Overloading resolution always happens at compile time.

			Runtime errors like NullPointerException can happen inside the method, not during selection.

✨ BONUS — How to fix ambiguity manually?

			If you want to fix it, you have to type cast explicitly.

			obj.show((StringBuffer) null);   // Force compiler to choose StringBuffer version
	or


			obj.show((StringBuilder) null);   // Force compiler to choose StringBuilder version
			
			✅ Then no ambiguity.

🎯 VERY Important Interview Tip

			When interviewer asks:

			"Will it throw exception or compile-time error when overloaded methods match equally with null?"

			✅ Answer: It throws a Compile-Time Error because of ambiguity.

🧠 Would you also like me to show how this concept is different in Method Overriding and why overriding never causes ambiguity?
(it's super helpful in senior interviews!) 🚀
👉 Should I continue?


			❓ When do you get AMBIGUITY ERROR with primitive types?
			
👉 You get ambiguity error when Java cannot clearly decide which method to call, because of widening between primitive types.

⚡ Example 1: No Ambiguity (Normal Working)

			public class PrimitiveExample1 {
				void show(int a) {
					System.out.println("int method");
				}

				void show(long a) {
					System.out.println("long method");
				}

				public static void main(String[] args) {
					PrimitiveExample1 obj = new PrimitiveExample1();
					obj.show(10); // Output: int method
				}
			}
			
			
			✅ No ambiguity here: 10 is int by default.

⚡ Example 2: AMBIGUITY (With Widening)

			public class PrimitiveExample2 {
				void show(int a) {
					System.out.println("int method");
				}

				void show(double a) {
					System.out.println("double method");
				}

				public static void main(String[] args) {
					PrimitiveExample2 obj = new PrimitiveExample2();
					obj.show(10L); // passing long
				}
			}
			
🔎 What happens here?

			10L is of type long.

			But there is no show(long) method!

			So compiler tries:

			Can long fit into int? ❌ (narrowing — not allowed automatically)

			Can long fit into double? ✅ (widening allowed)

			✅ So it will call show(double) without error.

📚 When Real Ambiguity Happens?

			Example 3: REAL AMBIGUITY with smaller types


			public class PrimitiveAmbiguity {
				void show(byte a, int b) {
					System.out.println("byte,int method");
				}

				void show(short a, long b) {
					System.out.println("short,long method");
				}

				public static void main(String[] args) {
					PrimitiveAmbiguity obj = new PrimitiveAmbiguity();
					obj.show((short) 10, 20); // ❓
				}
			}
			
🔎 What's happening:

			(short)10 is short.

			20 is int.

			But neither show(byte,int) nor show(short,long) is perfect match.

			Java will try to widen types to match.

			Now both methods are somewhat fitting by widening.

			Result: AMBIGUITY error ❌

			✅ This will cause compile-time ambiguity error like:


			reference to show is ambiguous
			both method show(byte,int) and show(short,long) match
			🧠 Widening Rules that Java follows internally:

			From	To (Allowed)
			byte	short → int → long → float → double
			short	int → long → float → double
			char	int → long → float → double
			int	long → float → double
			long	float → double
			float	double
			🚫 Narrowing (like long → int) is NOT automatic, needs explicit casting.

🎯 SUMMARY TABLE

			Situation	Result
			
			Exact match method	That method called
			No exact match → widening possible	Widened method called
			Multiple widenings possible equally	Ambiguity compile-time error
			No matching method and no widening possible	Compile-time error (method not found)
			
🚀 QUICK QUICK Example (Final Fast One)

			void show(int a) { }
			void show(float a) { }

			obj.show(10); 
			✅ Here 10 matches int first, so show(int) called.

			But if show(long) and show(float) both available and you pass int, both can accept int by widening, now ambiguous ❗.

✨ Final Interview Tip

			❝ If primitive type overloading results in multiple valid widenings at the same level, Java will throw Compile-Time Ambiguity Error. ❞




