# Lab02-data-structre-and-algotithem



package com.company;

public class Main {

    public static void main(String[] args) {
        SLL<String> fruitList  = new SLL<String>();
        String[] a = new String[]{"Mango", "Avocado", "Lime", "Peach", "Apple"};
        for (int i =0 ; i<a.length;i++) {
            fruitList.addToTail(a[i]);
            System.out.print(String.format("after inserting %s ",a[i]+" the list is>> "));
            fruitList.printAll();
        }
        System.out.print("after inserting fruit before Apple>> ");
        fruitList.insertBefore("fruit","Apple");
        fruitList.printAll();
        System.out.println( "the length of the list is "+fruitList.length());
        System.out.print("after inserting Watermelon after Lime>> ");
        fruitList.insertAfter("Watermelon","Lime");
        fruitList.printAll();
        System.out.print("after Deleting before Lime>> ");
        fruitList.deleteBefore("Lime");
        fruitList.printAll();
        System.out.print("after Deleting before mango>> ");
        fruitList.deleteBefore("Mango");
        fruitList.printAll();
        System.out.print("after deleting after Apple>> ");
        fruitList.deleteAfter("Apple");
        fruitList.printAll();
        System.out.println( "the length of the list is "+ fruitList.length());
        System.out.print("after deleting after Mango>> ");
        fruitList.deleteAfter("Mango");
        fruitList.printAll();
        System.out.print("after Deleting before Apple>> ");
        fruitList.deleteBefore("Apple");
        fruitList.printAll();
        System.out.println( "the length of the list is "+fruitList.length());

    }}






 class SLL<T> {
    protected SLLNode<T> head, tail;
    public SLL() {
        head = tail = null;
    }
    public boolean isEmpty() {
        return head == null;
    }
    public void addToHead(T el) {
        head = new SLLNode<T>(el,head);
        if (tail == null)
            tail = head;
    }
    public void addToTail(T el) {
        if (!isEmpty()) {
            tail.next = new SLLNode<T>(el);
            tail = tail.next;
        }
        else head = tail = new SLLNode<T>(el);
    }
    public T deleteFromHead() { // delete the head and return its info;
        if (isEmpty())
            return null;
        T el = head.info;
        if (head == tail)       // if only one node on the list;
            head = tail = null;
        else head = head.next;
        return el;
    }
    public T deleteFromTail() { // delete the tail and return its info;
        if (isEmpty())
            return null;
        T el = tail.info;
        if (head == tail)       // if only one node in the list;
            head = tail = null;
        else {                  // if more than one node in the list,
            SLLNode<T> tmp;    // find the predecessor of tail;
            for (tmp = head; tmp.next != tail; tmp = tmp.next);
            tail = tmp;        // the predecessor of tail becomes tail;
            tail.next = null;
        }
        return el;
    }
    public void delete(T el) {  // delete the node with an element el;
        if (!isEmpty())
            if (head == tail && el.equals(head.info)) // if only one
                head = tail = null;       // node on the list;
            else if (el.equals(head.info)) // if more than one node on the list;
                head = head.next;    // and el is in the head node;
            else {                    // if more than one node in the list
                SLLNode<T> pred, tmp;// and el is in a nonhead node;
                for (pred = head, tmp = head.next;
                     tmp != null && !tmp.info.equals(el);
                     pred = pred.next, tmp = tmp.next);
                if (tmp != null) {   // if el was found;
                    pred.next = tmp.next;
                    if (tmp == tail) // if el is in the last node;
                        tail = pred;
                }
            }
    }
    public void printAll() {
        for (SLLNode<T> tmp = head; tmp != null; tmp = tmp.next)
            System.out.print(tmp.info + " ");
        System.out.println();
    }
    public boolean isInList(T el) {
        SLLNode<T> tmp;
        for (tmp = head; tmp != null && !tmp.info.equals(el); tmp = tmp.next);
        return tmp != null;
    }


    public int length(){
        if (this.isEmpty())
            return 0;
        else {
             int i=1;
            SLLNode<T> temp = head;
            while (temp.next != null) {
                temp = temp.next;
                i++;
            }
            return i;
        }
    }




    public void insertBefore(T newElem, T existingElem){
        if(this.isEmpty()) {
            System.out.println("the linked list is empty");
            return;
        }
        else {
            if (head.next==null){
                SLLNode<T> newNode = new SLLNode<T>(newElem, head);
                head=newNode;
            }else{
                SLLNode<T> temp = head;
                SLLNode<T> prev = new SLLNode<T>(null, head);

                while (prev.next != null) {
                    if (temp.info == existingElem) {
                        //create a node before
                        SLLNode<T> newNode = new SLLNode<T>(newElem, temp);
                        if (prev.info == null) {
                            //this is the case to be the head
                            head = newNode;
                            return;
                        } else {
                            prev.next = newNode;
                            return;
                        }
                    } else {
                        // see another
                        prev = temp;
                        temp = temp.next;
                    }

                }
                System.out.println("the element does not exist");
            }
        }


    }


    public void insertAfter(T newElem, T existingElem) {
        if (this.isEmpty())
            System.out.println("the linkedList is empty");
        else {
            if (head.next==null){
                SLLNode<T> newNode = new SLLNode<T>(newElem, null);
                head.next=newNode;
            }else{
                SLLNode<T> prev = new SLLNode<T>(null, head);
                SLLNode<T> temp = head;
                while(prev.next!=null){
                    if (temp.info==existingElem) {
                        SLLNode<T> newNode = new SLLNode<T>(newElem, temp.next);
                        temp.next=newNode;
                        return;
                    }
                    else
                        prev=temp;
                        temp=temp.next;

                }
                System.out.println("the element does not exist");
            }
        }
    }

    public void deleteBefore(T existingElem){
        if (this.isEmpty())
            System.out.println("the Linkedlist is already empty ");
        else if (head.next==null){
            if (head.info==existingElem){
                System.out.println("there is no element before this element");
            }else
                System.out.println("existingElem does not exist  ");
        }
        else {
            SLLNode<T> temp = head;
            SLLNode<T> prev = new SLLNode<>(null,head);
            SLLNode<T> prev2 = new SLLNode<>(null,head);
            if (head.info==existingElem){
                System.out.println("there is no element before this element");
            }else {

                while (prev.next != null) {
                    if (temp.info == existingElem) {
                        prev2.next=temp;
                        if (prev==head){
                            head=temp;
                        }
                        return;

                    }else {
                        prev2=prev;
                        prev=temp;
                        temp=temp.next;

                    }

                }
            }
        }






    }



    public void deleteAfter(T existingElem){
        if (isEmpty())
            System.out.println("the linkedList is empty ");
        else if (this.head.next==null) {
            if (head.info == existingElem)
                System.out.println("there is no element after to delete");
            else
                System.out.println("the element does not exist");
        }
        else {
            SLLNode<T> temp = head;
            SLLNode<T> prev = new SLLNode<T>(null,head);
            while (prev.next!=null){
                if (temp.info==existingElem){
                    if(prev.next==this.tail){
                        System.out.println("there is no element after this element ");
                        return;
                    }else {
                        prev=temp;
                        temp.next=temp.next.next;
                        return;
                    }



                }

                prev=temp;
                temp=temp.next;


            }

        }
    }











}

//************************  SLLNode.java  *******************************
//           node in a generic singly linked list class

    class SLLNode<T> {
        public T info;
        public SLLNode<T> next;
        public SLLNode() {
            this(null,null);
        }
        public SLLNode(T el) {
            this(el,null);
        }
        public SLLNode(T el, SLLNode<T> ptr) {
            info = el; next = ptr;
        }
    }
