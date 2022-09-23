Conversion from Rx Observable to Concrete type

originalTypedObject.map { object -> Observable<NewType> 
    // object is a non-rx type
    // Mutate the type any way you want here in normal Swift code
    // Return a new type to sent it back to the observable sequence as the new type/object
}

