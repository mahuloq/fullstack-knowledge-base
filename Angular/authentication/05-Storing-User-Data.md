# Store user data in a model

export class User {
constructor(
public email: string,
public id: string,
private \_token: string,
private \_tokenExpirationDate: Date
) {}

get token() {
if (!this.\_tokenExpirationDate || new Date() > this.\_tokenExpirationDate) {
return null;
}
return this.\_token;
}
}

# Capture that user data from signing up and logging in. Not sure why you capture the info on signup, or if it even gives you that info.

export interface AuthResponseData {
kind: string;
idToken: string;
email: string;
refreshToken: string;
expiresIn: string;
localId: string;
registered?: boolean;
}

@Injectable({ providedIn: 'root' })
export class AuthService {
user = new Subject<User>();

constructor(private http: HttpClient) {}

signUp(email: string, password: string) {
return this.http
.post<AuthResponseData>(
'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyAsYk5fP-Ilfbvjgf6Fw-xRLZqulMffK-g',
{
email: email,
password: password,
returnSecureToken: true,
}
)
.pipe(
catchError(this.handleError),
tap((resData) => {
this.handleAuthentication(
resData.email,
resData.localId,
resData.idToken,
+resData.expiresIn
);
})
);
}

login(email: string, password: string) {
return this.http
.post<AuthResponseData>(
'https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=AIzaSyAsYk5fP-Ilfbvjgf6Fw-xRLZqulMffK-g',
{
email: email,
password: password,
returnSecureToken: true,
}
)
.pipe(
catchError(this.handleError),
tap((resData) => {
this.handleAuthentication(
resData.email,
resData.localId,
resData.idToken,
+resData.expiresIn
);
})
);
}

private handleAuthentication(
email: string,
userId: string,
token: string,
expiresIn: number
) {
const expirationDate = new Date(new Date().getTime() + expiresIn \* 1000);
const user = new User(email, userId, token, expirationDate);
this.user.next(user);
}

}
