```java
public class DigitCancellingFractions {
    public static void main(String[] args) {
        Fraction product=new Fraction(1,1);
        for (int num=10;num<100;num++){
            for (int den=num+1;den<100;den++){
                int x=num/10;
                int y=num%10;
                int b=den/10;
                int c=den%10;
                Fraction fraction = new Fraction(num,den);
                if(y==c&&y==0){
                    continue;
                }
                if(x==c && b>y &&fraction.reduce().equals(y,b)){
                    System.out.println(fraction);
                    product=product.multiply(fraction);
                }else if(x==b && c>y  &&fraction.reduce().equals(y,c)){
                    System.out.println(fraction);
                    product=product.multiply(fraction);
                }else if(y==b && c>x&&fraction.reduce().equals(x,c)){
                    System.out.println(fraction);
                    product=product.multiply(fraction);
                }else if(y==c && b>x && fraction.reduce().equals(x,b)){
                    System.out.println(fraction);
                    product=product.multiply(fraction);
                }

            }
        }
        System.out.println(product.reduce().getDenominator());
    }
}
```
```java
import java.util.Objects;

public class Fraction {
    private Integer numerator;
    private Integer denominator;


    public Fraction(int numerator, int denominator) {
        this.numerator = numerator;
        this.denominator = denominator;
    }

    public Fraction reduce(){
        int num=numerator/gcd(numerator,denominator);
        int dec=denominator/gcd(numerator,denominator);
        return new Fraction(num,dec);
    }

    public String toString(){
        return "("+numerator+"/"+denominator+")";
    }
    int gcd(int a, int b){
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }
    int lcm(int a,int b){
        return a*b / gcd (a,b);
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        return ((Fraction) o).numerator==numerator&&((Fraction) o).denominator==denominator;
    }

    public boolean equals(int num,int den){
        if (num==0||den==0) return false;
        return this.equals(new Fraction(num,den).reduce());
    }

    @Override
    public int hashCode() {
        return Objects.hash(numerator, denominator);
    }

    public Integer getDenominator() {
        return denominator;
    }

    public Fraction multiply(Fraction fraction){
        return new Fraction(this.numerator*fraction.numerator,this.denominator*fraction.denominator);
    }
}
```
