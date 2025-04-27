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
			Return 	Type		Can be different	Must be same/covariant
			Timing				Compile-time		Runtime
			Polymorphism Type	StaticPolymorphism	Dynamic Polymorphism
			
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

