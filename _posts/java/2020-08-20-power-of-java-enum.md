---
layout: post
title: "The Power of Java Enum - Factory Design Pattern"
preview: "Java Enums are a powerful tool, let's use them to create an instance of a class with factory design pattern."
image: /assets/images/unsplashed/windturbine.jpg
date: 2020-08-20 13:10:12 +0300
categories: java
---

Java Enums are a powerful tool, let's use them to create an instance of a class with factory design pattern.

```java
public enum Document {
	TEXT {
		@Override
		public IDocument getNewInstance() {
			return new TextDocument();
		}
	},
	WORD {
		@Override
		public IDocument getNewInstance() {
			return new WordDocument();
		}
	};

	/**
	 * @return IDocument new instance of specific IDocument
	 */
	public abstract IDocument getNewInstance();
};

public interface IDocument {
	String getTitle();
}
```

Create a list of document instances:

```java
private static List<IDocument> createDocuments(List<Document> docTypes){
	return docTypes.stream()
			.map(Document::getNewInstance)
			.collect(Collectors.toList());
}
```

Pros:

- Loose coupling, depend on abstractions, not concrete implementations;
- Control the types of instances that are created;
- Lazy instantiation, use the enum value until you need the concrete object to be created.
- Clean and concise code.

Cons:

- The instantiation method is a generic one and will depend on the same parameters, regardless of the specific object that needs to be created.
